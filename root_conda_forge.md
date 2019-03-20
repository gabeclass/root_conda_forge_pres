---
title: |
  Conda: a complete reproducible ROOT environment in under 5 minutes
author:
  - Henry Schreiner\inst{1,2}
  - Chris Burr\inst{3}
  - Enrico Guiraud\inst{4}
shortauthor:
  - H. Schreiner
  - C. Burr
  - E. Guiraud
institute:
  - University of Cincinnati\inst{1}
  - Princeton University\inst{2}
  - University of Manchester\inst{3}
  - CERN\inst{4}
date: March 21, 2019
fontsize: 10pt
aspectratio: 169
---



# Getting Conda

Download through <https://www.anaconda.com/distribution/>, graphical installers, your favorite package manager, or the following lines (command line or servers):

**Download the Linux installer**
```bash
wget -nv http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
     -O miniconda.sh
```

**Or download the macOS installer**
```bash
wget -nv https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh \
     -O miniconda.sh
```

**Install Conda (same for macOS and Linux)**
```bash
bash miniconda.sh -b -p $HOME/miniconda
```

**Activate, add to bashrc** - similar files available for fish and csh
```bash
source $HOME/miniconda/etc/profile.d/conda.sh
```

# Install ROOT anywhere
**New environment:**

```bash
conda create -n myrootenv python=3.7 root -c conda-forge
conda activate myrootenv
conda config --env --add channels conda-forge
```

**Inside an environment:**

```bash
conda config --env --add channels conda-forge
conda install root
```

# Features

If you've heard of the NLeSC ROOT package, this is the successor:

::: columns
::: column

* Full featured ROOT (not just PyROOT)
    - Compile your own code with C++17
    - Full graphics
    - JupyROOT
    - No environment setup needed
* Full support for Linux and macOS
    - Testing in ROOT nightlies planned
    - Tested on many distributions
* Supports Python 3.7, 3.6, and 2.7

:::
::: column

* Uses external packages where possible
* Many optional features activated
    * Minuit2
    * RooFit
    * Pythia8
    * And more!

:::
:::

##
Note: macOS requires 10.9 SDK for now - restriction should be lifted in the future.

# Building

* Conda-forge automation: CI builds and bots help with updates
* Using new uniform compiler stack
    - ROOT became available almost on day 1 of the new compilers
* Recipe and patches are at \github{conda-forge/root-feedstock}





# Development
* Quite a few patches accepted into ROOT 6.16.00, 6.16.02, and 6.18.00


# Usage examples: Reproducible and shareable environments

::: columns
::: column

* Can mix ROOT with TensorFlow or PyTorch on GPU
* Can run Multiple Python versions and ROOT


Run with:

```bash
conda create -f environment.yml
```

:::
::: column

```yml
name: pvfindergpu
channels:
    - pytorch
    - conda-forge
dependencies:
    - python>=3.6
    - root
    - pythia8
    - pandas
    - jupyterlab
    - uproot
    - h5py
    - numba
    - scipy
    - matplotlib
    - pytorch
    - cudatoolkit=9.0
```

:::
:::

# Reproducible and shareable environments: continued


```bash
conda env export > environment.yml
```

<!--
## Perfect reproduction
The above is probably fine, but if you really want to store the exact packages:
```bash
conda list --explicit > spec-file.txt
```
followed by
```bash
conda create --name myenv --file spec-file.txt
```
will perfectly recreate an environment on the same OS.
:::
::: column
-->

```yml
name: pvfindergpu
channels:
  - pytorch
  - conda-forge
  - defaults
dependencies:
  - afterimage=1.21=hf014aae_1002
  - asn1crypto=0.24.0=py37_1003
    ...
  - root=6.16.00=py37_blas_openblash629dc00_5
  - scipy=1.2.1=py37_blas_openblash1522bff_0
    ...
  - zlib=1.2.11=h14c3975_1004
prefix: /home/schreihf/.conda/envs/pvfindergpu
```

# Usage examples: MyBinder

::: columns
::: column


[Aghast](https://github.com/diana-hep/aghast) [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/diana-hep/aghast/binder-3?filepath=binder%2Fexamples.ipynb)

```
environment.yml
```

```yml
channels:
  - conda-forge
dependencies:
  - root
  - pandas
  - numpy
  # for flatc code generator
  - flatbuffers>=1.8.0
  - pip:
      # for Python flatbuffers runtime
      - flatbuffers>=1.8.0
```

:::
::: column
[tcanvasmagic](https://github.com/olantwin/tcanvasmagic) [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/olantwin/tcanvasmagic/master?filepath=demo.ipynb)

```
environment.yml
```

```yml
channels:
  - conda-forge
dependencies:
  - root
```

:::
:::

# Other

## CI

* Uproot now tests against ROOT on Travis CI using Conda.
* Many SciKit-HEP packages now can/are adding support for ROOT in testing.
* Simple to add to any CI system

## Docker

* You can use the docker image for Conda to setup ROOT!
* Recipe for pre-configured ROOT on Conda docker available


\backupbegin

# Backup 

## 
This is a backup slide

\backupend
