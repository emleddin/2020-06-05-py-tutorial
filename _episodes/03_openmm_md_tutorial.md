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
angle_restraints = HarmonicAngleForce()
~~~
{: .language-python}

{% include links.md %}
