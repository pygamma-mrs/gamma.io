---
sort: 1
---

# Overview

We (the Vespa team) took over maintenance of a dormant GAMMA late in 2009. It had probably been about six years since GAMMA was actively advanced, and it took us some time to get GAMMA to compile with modern compilers. We also added the SWIG interface, which is entirely new.

These documents contain some notes from that time when we were working on releasing our first version which was GAMMA 4.2.0.

- [**GAMMA/GAMMA Contributors**](GammaContributors.md) - Singing the unsung!
- [**GammaSwigImplementation**](../technical/gamma/GammaSwigImplementation.md) - Swig Implementation notes, including organization of code, some (potentially remaining) issues, and Makefile and visual-studio modifications.
- [**GammaMergerwithZurich**](GammaMergerwithZurich.md) - Merging C++ code with that from Zurich (Matthais Ernst), changes, issues, etc.
- [**CodeCleanup**](CodeCleanup.md) - Code Cleanup Notes. Those who were familiar with the old version of GAMMA might be interested in some of the files we got rid of.
- [**CodeChangesToCompile**](../technical/gamma/CodeChangesToCompile.md) - Changes we made to get GAMMA to compile on gcc 4.3.3 (on Ubuntu 9.04), Visual Studio 2008 Express (Windows XP), and gcc 4.0.1 (Mac OSX).
- [**GammaSwigIssues**](../technical/swig/GammaSwigIssues.md) - Found while getting environment setup and testing the basic functionality of SWIG. While using gcc 4.3.3/Ubuntu 9.04/Swig 1.3.9/python2.5 and 2.6

