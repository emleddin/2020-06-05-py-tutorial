---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---
This workshop was designed to go over the basics of molecular dynamics (MD)
simulations with OpenMM, and using MDAnalysis for trajectory analysis.


My brief outline:
- Loading in universe
- Atom groups and residue groups
- Trajectory information and why it's hell
- Setting up analysis
    - Autoimage
- Using Pandas?
- Pandas and matplotlib?
- Example with different types of files (PDB, XYZ, TXYZ, Prmtop/Inpcrd)

<!-- this is an html comment -->

{% comment %} This is a comment in Liquid {% endcomment %}
{% comment %} > [lesson 3]({{ page.root }}{% link _episodes/03-using-openmm.md %}), {% endcomment %}

> ## Prerequisites
>
> Students should be familiar with using the Terminal to execute commands,
> as well as creating and editing text files.
> The workshop was designed to start from FIXME.
> Lessons 1-2 contain additional background information for
> students that are  unfamiliar with biomolecular simulation and/or Python.
{: .prereq}

{% include links.md %}
