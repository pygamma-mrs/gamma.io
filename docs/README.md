---
sort: 1
---

# The PyGAMMA/GAMMA Package

## Welcome to the PyGAMMA/GAMMA Library

**GAMMA** is a C++ library for the simulation of magnetic resonance (NMR, MRS) experiments. It provides a simple and intuitive means to construct simulation programs to suit researchers' individual needs. GAMMA is an acronym for a ** *G*eneral *A*pproach to *M*agnetic resonance *M*athematical *A*nalysis **.

**PyGamma** is a Python wrapper around GAMMA that makes almost all of GAMMA's API available via [Python](http://www.python.org/). PyGamma users can skip the C++ compile and link steps and can even run GAMMA commands interactively line-by-line.

Both PyGamma/GAMMA and  work on OS X, Linux, and Windows.

For more information, refer to our [detailed description of GAMMA](../docs/technical/gamma/GammaDetailedDescription.md) and our [main PyGamma page](../docs/installing/PyGamma.md).


## How To Get GAMMA and PyGamma

We have [instructions on how to download and build GAMMA](../docs/release/GammaBuildingLibrary.md).

You can [install PyGamma with Python's pip](../docs/installing/PyGamma.md).

## Documentation

The original documentation written by Scott Smith in the [browser:/trunk/doc/pdf gamma/doc/pdf] directory of the GAMMA source code distribution.

The PDFs include a user manual, and one document each for most GAMMA modules. These documents are somewhat dated. Nevertheless, they serve as a useful reference to what the library can do, and how to do it.

We also supply C++ examples in in the [browser:trunk/src/Tests gamma/src/Tests] folder, and Python examples in [browser:trunk/src/pyTests gamma/src/pyTests].

For the very ambitious, we have [archived the HTML from the old GAMMA Web site](http://scion.duhs.duke.edu/guest_svn/gamma_docs/trunk/).


## Developer (Technical) Documentation

If you're interested in more technical details about GAMMA/PyGamma including notes from the developers themselves, or suggestions on how to contribute to PyGAMMA/GAMMA, we have a whole section dedicated to [developer documentation](../docs/technical/README.md).


## Proper Citation in Papers and Presentations
Proper reference should be given, using the citation below, when GAMMA simulations are used in papers and/or presentations.

"Computer Simulations in Magnetic Resonance. An Object Oriented Programming Approach", S.A. Smith, T.O. Levante, B.H. Meier, and R.R. Ernst, J. Magn. Reson., 106a.


## Thanks
Thanks to the ** *NIH* (*grant number 1R01EB008387-01A1*) ** which funded the recent work on PyGAMMA/GAMMA and this website via the [Vespa project](http://github.com/vespa-mrs/vespa).

Thanks also to those who have [contributed their time and skills](../docs/history/GammaContributors.md) to PyGAMMA/GAMMA.
