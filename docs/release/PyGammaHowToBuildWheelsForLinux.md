---
sort: 2
---

# Build PyGamma Wheels (Linux)

This document describes how to build PyGamma wheels for Linux.

## Introduction

Building wheels for Linux requires some care. Fortunately, the PSF has researched the topic and made suggestions on how to avoid some of the pitfalls. That's summarized in PEP 513, PEP 571 and [PEP 599](https://www.python.org/dev/peps/pep-0599/).

When the PyGamma project began, we made use of PEP 513 rules to create Linux binaries for Python 2.7 but since 2019 we have followed PEP 599 and the 'manylinux2014' rules that user compilation under CentOS 7.

PEP 599 identifies CentOS 7 as the benchmark system on which a wheel should work for it to be broadly compatible. The easiest way to ensure that the PyGamma binaries run on CentOS 7 is to build them there. Wheels created according to these rules typically have 'manylinux2014' in their name scheme.

You may also want to look at [PEP 600](https://www.python.org/dev/peps/pep-0600/) for ongoing 'manylinux' information. In short, this effort has changed over to a naming scheme that depends on the glibc version to differentiate wheels.

- (deprecated) PEP 513 identifies CentOS 5.11 as the benchmark system on which a wheel should work for it to be broadly compatible. The easiest way to ensure that the PyGamma binaries run on CentOS 5.11 is to build them there. Wheels created according to these rules typically have 'manylinux1' in their name scheme.
- (deprecated) NB. PEP 513 was updated to [PEP 571](https://www.python.org/dev/peps/pep-0571/)
- (deprecated) PEP 571 identifies CentOS 6 as the benchmark system on which a wheel should work for it to be broadly compatible. The easiest way to ensure that the PyGamma binaries run on CentOS 6 is to build them there. Wheels created according to these rules typically have 'manylinux2010' in their name scheme.
- (deprecated) NB. PEP 571 was updated to [PEP 599](https://www.python.org/dev/peps/pep-0599/)


If you don't already have a CentOS 7 virtual machine, now is the time to build one. There are instructions on 
[ how to set up a CentOS VM](../developer/PyGammaHowToSetUpCentOs).

## Build PyGamma

1. Get the GAMMA source code onto your CentOS machine via SVN or any other way
 you like.
1. `cd gamma/platforms/Linux`
1. `make pysgdist`
1. `cd ../../pygamma`
1. `python setup.py bdist_wheel`

The last step creates the wheel file in the `dist` directory. As of this writing, the wheel package doesn't know about the `manylinux2014` standard described in PEP 513, so the wheel is inappropriately named. For instance, the wheel I created was named this --
```
pygamma-4.3.3-cp27-cp27mu-linux_x86_64.whl
```
I manually renamed it to this -- 
```
pygamma-4.3.3-cp27-cp27mu-manylinux2014_x86_64.whl
```

You might also need to rename the wheel you create.

## Testing the Wheel

1. (optional) In the `gamma/pygamma/dist` directory, type `pip uninstall pygamma` to remove current package
1. In the `gamma/pygamma/dist` directory, type `pip install <wheel name>` to install package
1. (optional) You may need to run dos2unix on the \*.sys and \*.txt files in `gamma/src/PyTests`
1. Change to `gamma/src/PyTests` directory, type `python ../Tests/run_tests.py -v `
1. PyGamma test results will print out in cmd window



## Notes about the Linux Makefile

March 2020. We have set the Linux SWIG options to be just -c++ -python and removed the -builtin option. It was causing the pythoncode extensions I added to enable python print() to be useful with pygamma objects to not be included in the pygamma.py wrapper file.  We have also excluded the -py3 option at this time until we completely remove support for python 2.x 

## Why CentOS 7? (Optional Reading)

CentOS is a Red Hat EL derivative, and Red Hat is a very conservative distro. CentOS 7 was released in
September of 2014, which means it's an old-ish version of a conservative distro. That means the runtime libraries on that system are a least common denominator of just about any Linux system likely to be in use. If a binary can run there, it should run just about anywhere. CentOS 7 will reach end of life in 2024.
