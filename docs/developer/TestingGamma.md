---
sort: 3
---

# Testing GAMMA and PyGAMMA

Procedures for testing a build, to guarantee that you didn't break anything (or at least that you didn't break anything that is being tested). Here are the steps that are used to make sure that nothing major is broken...

## To Do

1. *Add more tests. If we have more tests we'll be better off.*
1. *Add unit tests.*

## Testing Plan for Linux (and OSX)

The following sequence of builds and tests should work without any issues. You may need to be sudo or root to execute some of these items. 

Select items on this list require a working version of Python (>= 2.5) to be installed, and are marked with a (P). And some items require Swig (S). 

Go to the build instructions for [GAMMA](/wiki:GammaBuildingLibrary/) and [PyGAMMA](/wiki:PyGamma#BuildingPyGAMMA/) for details.

We're assuming you start in the gamma/platforms/Linux or gamma/platforms/OSX directory.

  * make all
  * make install
  * make test (P)
  * make pysgdist (P,S)

  * Install and test pygamma (P)
    * cd ../../pygamma
    * python setup.py install
    * open up a python shell and try to "import pygamma"
    * from within that shell try "c = pygamma.complex(3,4)"
    * and thev confirm that c is a swig object. i.e. c <enter>
    * exit python.
    * cd ../platforms/Linux

  * Test gamma utility
    * cd  ../../src/Tests
    * gamma par_xixA.cc
    * ./a.out
    * make sure this at least begins to run, and asks for user input.
    * control-C
    * cd ../platform/Linux

  * make pytest (P)


# Notes on How We Developed out Tests and PyTests Process

We needed a simple set of tools for building and running test code, and for evaluating and reporting the success of the results.

It needed to do all of the following:
  * Build Test Code.
  * Run test code and make sure no errors.
  * Compare output files with some verified standard.
  * Compare stdout with a verified standard (golden file).
  * Read and manage input files (for test cases).

## Note on unit testing

- Evaluated the code in the src/Testing directory. It is basically a testing harness but seemed too complex for our needs.  
- Also Evaluated 3rd party testing tools.  I was impressed by Google's C++ testing framework, and was also intrigued by CppUnit and CxxTest. If I was going to do ongoing development I would have gone further in this direction, but since we are moving more toward the python world, learning a new testing tool was not a priority at this time.  However, if there is more development work on the C++ version of the code, then one of these, or it's replacement would be worth considering.  Wikipedia has a good listing of C++ unit testing tools: http://en.wikipedia.org/wiki/List_of_unit_testing_frameworks#C.2B.2B