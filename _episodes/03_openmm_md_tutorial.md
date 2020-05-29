---
title: "OpenMM"
teaching: 0
exercises: 0
questions:
- "How do you set up an OpenMM molecular dynamics simulation in Python?"
- "What information can OpenMM provide as the simulation is running?"
objectives:
- "Load simulation inputs into Python."
- "Set up simulation parameters and environments."
- "Apply distance and angle restraints."
- "Set up outputs and reporters."
- "Run short trajectory of molecular dynamics."
- "Restarting a simulation from a checkpoint."
keypoints:
- "OpenMM in Python can make use of GPUs to perform molecular dynamics simulations."
---

There is an
[OpenMM tutorial site](http://openmm.org/tutorials/index.html) with some additional "cookbook" style tutorials.
This is meant as an introduction to the basics.

## Importing OpenMM into Python

This portion assumes you have already installed the appropriate version of OpenMM to your specific environment.  OpenMM is CUDA-compatible, and [different versions](https://anaconda.org/omnia/openmm) are available depending on which version of CUDA you're using.

~~~
import simtk as omm
from simtk.openmm.app import *
from simtk.openmm import *
from simtk.unit import *
from simtk.openmm import app
~~~
{: .language-python}

## Loading Simulation Inputs

We assume you have already generated your .prmtop and .inpcrd files for your system.  If you haven't, use the example files provided.
Also, remember that assigning variables, classes, and objects in python is very important.

~~~
prmtop = app.AmberPrmtopFile("protein.prmtop")
inpcrd = app.AmberInpcrdFile("protein.inpcrd")
~~~
{: .language-python}


## Setting up the Simulation Environment

OpenMM requires several pieces of information to get started, but assigning variables in stages can help keep things organized (and also easy to modify for future use.)

~~~
platform = Platform.getPlatformByName('CUDA') #This assumes you're using a CUDA-enabled version of OpenMM
properties = {'CudaPrecision': 'mixed'}
system = prmtop.createSystem(nonbondedMethod = app.PME,         # Using Particle-mesh Ewald
                             nonbondedCutoff = 1.0\*nanometers, # with a 10 Angstrom cutoff distance
                             constraints = app.HBonds,          # keeping bonds between hydrogens and heavy atoms at a fixed length
                             ewaldErrorTolerance = 0.001,       # setting the error tolerance for the Ewald
                             rigidWater = False,                # letting waters be flexible instead of solid triangles
                             removeCMMotion = True              # maintains the center of the periodic box at the center of mass
~~~
{: .language-python}

You'll also want to set up your thermostat to run in NVT (and add a barostat to run in NPT).

~~~
thermostat = LangevinIntegrator(300\*kelvin, 1/picoseconds, 0.001\*picoseconds)
    # Temperature, Friction Coefficient, Timestep
    # This will be added to the larger simulation
    
barostat = MonteCarloBarostat(1.0\*atmosphere, 300.0*kelvin, 25)
    # Pressure, Temperature (only used for calculation), Frequency (how frequently the system should update the box size)
system.addForce(barostat)
    # The barostat is added directly to the system rather than the larger simulation.
~~~
{: .language-python}

If you need distance or angle restraints between atoms, you can add them here.

~~~
distance_restraints = HarmonicBondForce()
distance_restraints.addBond(index1, index2, distance\*angstroms,force\*kilocalories_per_mole/angstomrs\*\*2)
    # First atom index (python starts at zero!), Second atom index, Distance, Force Constant
    # You can use as many addBond() function calls as you like, if there are multiple distances to restrain.  
    # But be careful not to duplicate any, as they won't overwrite each other, just additively stack up.
system.addForce(distance_restraints)
    # Add the collection of distance restraints to your system.
    
angle_restraints = HarmonicAngleForce()
angle_restraints.addAngle(index1, index2, index3, angle, force\*kilocalories_per_mole/radians\*\*2)
    # First, second, and third atom indices, with the second atom as the vertex of the angle, the desired angle in radians, and the force constant.
    # As above, add as many angle restraints as you need, but be careful not to duplicate them.
system.addForce(angle_restraints)
    # Add the collection of angle restraints to the system.
~~~
{: .language-python}

Now we need to set up the entire simulation with what we've done so far.

~~~
sim = Simulation(prmtop.topology, # The topology of the system
                 system,          # The system itself, with all the restraints, barostat, etc.
                 thermostat,      # The thermostat, in this case the LangevinIntegrator we established before
                 platform,        # The CUDA environment
                 properties)      # Settings for the environment
sim.context.setPositions(inpcrd.getPositions(asNumpy=True))
    # Gets the starting position for every atom in the system and initializes the simulation
sim.context.getState(getPositions=True, enforcePeriodicBox=True).getPositions()
    # Establishes the periodic boundary conditions of the system based on the box size.
sim.reporters.append(StateDataReporter("output.log",            # filename to save the state data into.
                                       1000,                    # number of steps between each save.
                                       step = True,             # writes the step number to each line
                                       time = True,             # writes the time (in ps)
                                       potentialEnergy = True,  # writes the potential energy of the system (KJ/mole)
                                       kineticEnergy = True,    # writes the kinetic energy of the system (KJ/mole)
                                       totalEnergy = True,      # writes the total energy of the system (KJ/mole)
                                       temperature = True,      # writes the temperature (in K)
                                       volume = True,           # writes the volume (in nm^3)
                                       density = True))         # writes the density (in g/mL)
                                       
sim.reporters.append(CheckpointReporter("molecule.chk",10000))  # Updates the checkpoint file every 10,000 steps

sim.reporters.append(DCDReporter("trajectory.dcd",10000))       # Adds another frame to the CHARMM-formatted DCD (which can be easily 
                                                                # converted to .mdcrd by cpptraj) every 10,000 timesteps.
                                                                # It's good practice to keep the trajectory and checkpoint on the same
                                                                # write frequency, in case you need to stop a job and resume it later.
~~~
{: .language-python}

We have now set up the entire system for running molecular dynamics!  But first, as is good practice, we want to minimize the system first to clear any potential clashes between atoms and residues.

~~~
sim.minimizeEnergy(maxIterations=2000) 
~~~
{: .language-python}

You can set the maxIterations to whatever value you want, but be careful not to minimize for too long, as you can wind up starting from a structure that may be very different from your original files.
From here, you can begin the actual MD portion.

~~~
sim.step(1000000) #This instructs the program to take 1,000,000 timesteps, which corresponds to 1.0 ns of MD based on a 1fs timestep.
~~~
{: .language-python}

Be careful here, as this will write the entire trajectory to a single file as it goes.  It's a good idea to save backups along the way, especially if you're restarting from checkpoints.  Otherwise, the program will overwrite the file when you resume simulation, and you can lose the data.  

## Restarting a Simulation from a Checkpoint

Sometimes we may want to pick up a simulation where we left off.  This requires only some slight modifications to the process.  Most of the script you built above can be used, with a few exceptions.  First, **remove the following portion**, as we no longer want the starting positions determined by the .inpcrd file.

~~~
sim.context.setPositions(inpcrd.getPositions(asNumpy=True))
    # Gets the starting position for every atom in the system and initializes the simulation
~~~
{: .language-python}

Next, add this section immediately before declaring the checkpoint file to use going forward.

~~~
with open("restart.chk",'rb') as f:
    sim.context.loadCheckpoint(f.read())
~~~
{: .language-python}

You will also want to remove the line that minimizes the system, as you no longer want this to happen.  Afterwards, the rest of the script is the same.  You may notice that the "restart.chk" file is differently named than the normal checkpoint file we declared before.  You can technically use the same checkpoint file to restart and immediately begin overwriting, but this has its own risks in case something goes wrong.  By making a copy of the checkpoint and restarting from the copy, you have a separate backup that will allow for mistakes without losing data (Author speaks from painful experience here!)

At this point, you should be able to set up an OpenMM simulation from start to finish, including resuming a stopped simulation.

{% include links.md %}
