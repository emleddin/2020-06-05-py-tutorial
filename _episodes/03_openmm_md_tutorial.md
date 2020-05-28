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


{% include links.md %}
