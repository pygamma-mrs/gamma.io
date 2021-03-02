# New Install or Upgrade

## Overview

PyGamma is a Python-wrapped version of [GAMMA](../technical/gamma/GammaDetailedDescription.md). It combines the power of the GAMMA library with the convenience of working in [the Python programming language](http://www.python.org/). Python is open source, object-oriented, and considerably easier to write than C++. 

PyGamma works with Python 3.7. We no longer support Python 2.7 officially (but may create distributions anyway until we can't any longer).

The PyGamma wrapper was created using [SWIG](http://www.swig.org/). Most, but not all of GAMMA is [available to Python through PyGamma](../technical/pygamma/SwiggedGammaListing.md). 

We have are some [tips on exploring and using PyGamma](../technical/pygamma/PyGammaUsageTips/).

The [performance of PyGamma](../technical/performance/GammaVsPyGamma.md) for compute-intense calculations is very comparable to that of GAMMA.

## Installation Requirements

You must have pip installed to get PyGAMMA. 

If pip isn't installed, get it via the the instructions here:
https://pip.pypa.io/en/stable/installing/#installing-with-get-pip-py

We strongly recommend upgrading to the latest version of pip before installing pygamma.

To upgrade pip, use this command:
```
python -m pip install --upgrade pip
```

## New PyGAMMA Install

As of version 4.3.3, PyGamma is installable via pip, Python's preferred installer program. To install PyGamma, use this command:
```
pip install pygamma
```

## PyGAMMA Upgrade

To upgrade PyGamma, use this command:
```
pip install --upgrade pygamma
```
