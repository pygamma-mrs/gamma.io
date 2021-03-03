---
sort: 3
---

# Build PyGamma Wheels (OS X)

This document describes how to build PyGamma wheels for OS X.

## Introduction

This document assumes you are building a 64-bit PyGamma.

## Setup Compiler and Python

1. Install XCode to get the OS X build toolchain.
1. Ensure a modern 64-bit Python is in your path. 
 - I used the [Miniconda](https://docs.conda.io/en/latest/miniconda.html) 64 bit Python 3 installer script for OSX. 
 - Once miniconda is installed, use the `conda create --name python37 python=3.7` command to set up a python 3.7 environment. Change the name or python version as needed for your compile
 - (optional) You can also compile for any other Python version for which you set up an environment. 
1. Install the `wheel` package in your conda environment. One of the below steps should work:
 - `conda install wheel`
 - `conda install -c conda-forge wheel`
 - `pip install wheel`
1. Switch to the desired miniconda environment before doing the "Build PyGamma" steps below.

## Download and Build [SWIG](http://www.swig.org).

1. Download and untar the SWIG source code. I was able to use the latest (4.0.2 as of this writing).
1. Build with `sudo ./configure && sudo make && sudo make install`


## Build PyGamma

1. Get the GAMMA source code via SVN.
1. `cd gamma/platforms/OSX`
1. (optional) `make clean`          remove previous compile files
1. `make pysgdist`
1. `cd ../../pygamma`
1. `python setup.py bdist_wheel`

The wheel file will be in the `dist` directory.

Note that the OS X Makefile and PyGamma's setup.py contain some special code to ensure the PyGamma wheel automatically gets the correct name. 