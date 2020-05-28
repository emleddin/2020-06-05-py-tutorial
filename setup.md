---
title: Setup
---

## Obtain the Lesson Materials
All files have been made available
[on GitHub](https://github.com/emleddin/2020-06-05-files).
Click the green button labeled `Clone or download` and select `Download ZIP`.
Open the ZIP folder and move the files wherever you would like to work from.

## Using Google Colab for Python
Any of the code contained herein can be run using
[Google Colab](https://colab.research.google.com/notebooks/intro.ipynb).
You can install Python packages using `!pip install` in a code cell.
Colab notebooks are interactive Python notebook, much like Jupyter notebooks.

Any files that you need to use within a Colab notebook can be on your Google
Drive account.
For files the Drive, click the folder icon on the left of the code/text cells,
and select "Mount Drive."
If you don't want to link your Google Drive, you can select "Upload" instead.

### Highlights
* Text-based cells are written in Markdown
* Cells can be evaluated by `Shift+Enter`
* Lines can be easily commented with `Cntl+/` ( `Cmd+/` on Mac)

### Using Python Packages
A number of commonly used packages are already available for import in the
Google Colab environment, like `matplotlib`, `numpy`, and `pandas`.
Additional packages can be installed through `!pip install XXX` or
`!apt-get install XXX` where `XXX` is the name of the package to be installed.
Additional information about this can be found
[here](https://colab.research.google.com/notebooks/snippets/importing_libraries.ipynb).

## Installing Python (Anaconda) Locally

1. Go to the [Anaconda Download page](https://www.anaconda.com/products/individual).
2. Download the installer for your operating system. (You likely use 64-bit.)
**Make sure you get the Python 3 version.**
3. Double click the installer and follow the instructions.
All the default options are fine for MacOS and Linux. For Windows, be sure to
select `Make Anaconda the default Python` (the rest of the defaults are fine).

### Installing Anaconda Packages

Packages can be installed through `conda install XXX` where `XXX` is the
package name.
In certain cases, you have to specify a channel.

For OpenMM:
```
conda install -c omnia -c conda-forge openmm
```
{: .language-python}

For MDAnalysis:
```
conda config --add channels conda-forge
conda install mdanalysis
```
{: .language-python}

## AMBERTools for Structure Preparation

### Conda Installation of Tools Binaries

AMBERTools has added a Python-based installation for the tools binaries.
It should work for Linux and MacOS, but is not a true substitute for the
full AMBERTools code.
It is fine for the purposes of this tutorial.

```
conda install -c conda-forge ambertools
```
{: .language-python}

### Full Source Code

The full source-code can be downloaded from the
[AMBER website](https://ambermd.org/AmberTools.php).
This is the version that should be linked with an AMBER distribution.

{% include links.md %}
