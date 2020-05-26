---
title: "MDAnalysis"
teaching: 0
exercises: 0
questions:
- "How are structure and trajectory files read with Python?"
- "What is an atom group?"
objectives:
- "Load structures and trajectories into Python."
- "Use AtomGroups to make selections of atoms."
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

There is a
[real MDAnalysis tutorial](https://www.mdanalysis.org/MDAnalysisTutorial/index.html).
This is more of "highlights" lesson.

## The Universe System

<!-- - Example with different types of files (PDB, XYZ, TXYZ, Prmtop/Inpcrd) -->

~~~
import MDAnalysis as mda

system = mda.Universe(filename, in_memory=True)
~~~
{: .language-python}

### Memory with MDAnalysis

Talk about `in_memory=True` FIXME

> ## Load a Tinker XYZ
>
> Create a universe where you use a PDB file for the topology and a TINKER XYZ
> for the trajectory. Then, check the type and ensure it is a universe.
>
> > ## Solution for Loading a Tinker XYZ
> >
> > You can either define variables with the file names, or you can use them
> > directly in the command associated with them.
> >
> > ~~~
> > import MDAnalysis as mda
> >
> > ## in_PDB is the original PDB, in_txyz is the converted TINKER XYZ
> > in_pdb = "my_original.pdb"
> > in_txyz = "my_original.xyz"
> >
> > ## Read in the PDB as topology and TXYZ as "trajectory"
> > system = mda.Universe(in_pdb, in_txyz, format='TXYZ', in_memory=True)
> >
> > ## Check the type
> > type(system)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

## Atom Groups

## Residue Groups

## Setting Up Analysis

### What's autoimage look like?

## `pandas` and `matplotlib`


{% include links.md %}
