---
title: "Introduction to Python"
teaching: 0
exercises: 0
questions:
- "What are Python packages?"
- "How do I use variables?"
- "What are comments and docstrings?"
- "How do I write a function in Python?"
objectives:
- "Follow the common components of a Python code."
keypoints:
- "Use `import` to load in Python packages."
---

## Python Packages and the `import` Command
Packages are handy, well, packages of code that are designed with a specific
purpose.
For instance, `matplotlib` is a library built for data visualization.
The package just bundles it up all nicely into something that can be loaded,
like how `module load` works on an HPC cluster.
Thus, when you need to use a package for a specific purpose, you need to
`import` it into Python.

> ## Additional Resources for Getting Started with Python
>
> * [MolSSI Python Scripting for Computational Molecular Science](http://education.molssi.org/python_scripting_cms/)
> * [MolSSI Python for Data Analysis](https://education.molssi.org/python-data-analysis/)
> * [Python Crash Course Cheat Sheets](https://ehmatthes.github.io/pcc/cheatsheets/README.html)
> * [Software Carpentry Programming with Python](http://swcarpentry.github.io/python-novice-inflammation)
> * [Software Carpentry Plotting and Programming in Python](http://swcarpentry.github.io/python-novice-gapminder)
>
{: .callout}

> ## If You Learn One Thing About Python, We Hope It's This
>
> **Python starts indexing at 0 (zero).**
> This means that when working with arrays, the very first position is not 1,
> but 0.
>
> ~~~
> import numpy as np
> x_list = np.arange(0,10,1)
> print(x_list)
> for x in x_list:
>     print(f"I am number {x} of {len(x_list)}.")
> ~~~
> {: .language-python}
> ~~~
> [ 0 1 2 3 4 5 6 7 8 9]
> I am number 0 of 10.
> I am number 1 of 10.
> I am number 2 of 10.
> I am number 3 of 10.
> I am number 4 of 10.
> I am number 5 of 10.
> I am number 6 of 10.
> I am number 7 of 10.
> I am number 8 of 10.
> I am number 9 of 10.
> ~~~
> {: .output}
{: .callout}

{% include links.md %}
