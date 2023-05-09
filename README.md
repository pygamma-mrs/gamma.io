# Welcome to the PyGAMMA/GAMMA Documentation Repo

**GAMMA** is a C++ library for the simulation of magnetic resonance (NMR, MRS) experiments. It provides a simple and intuitive means to construct simulation programs to suit researchers' individual needs. GAMMA is an acronym for a ** *G*eneral *A*pproach to *M*agnetic resonance *M*athematical *A*nalysis **.

**PyGamma** is a Python wrapper around GAMMA that makes almost all of GAMMA's API available via [Python](http://www.python.org/). PyGamma users can skip the C++ compile and link steps and can even run GAMMA commands interactively line-by-line.

Both PyGamma/GAMMA and  work on OS X, Linux, and Windows.

## What Kind of Documentation is Here?

This repository is mainly a container for all the things we learned while adding the Python SWIG functionality to the original GAMMA C++ library.  It has Installation, Developer, Package Release, Technical and Historical sub-levels.  Much of this content was ported from a Trac repository and we are still in the process of weeding the files for GitHub Pages compliance. Thank you for your patience. 

This repository does not contain the original documentation (PDFs) written by Scott Smith from the 'docs' directory of the GAMMA source code distribution. That is a large amount of data and is currently stored elsewhere (link coming soon). Those PDFs include a user manual, and one document each for most GAMMA modules. Those documents are somewhat dated. Nevertheless, they serve as a useful reference to what the library can do, and how to do it.

## Citation

If you publish material that makes use of GAMMA, please cite the following publication:

Smith SA, Levante TO, Meier BH, and Ernst RR. Computer Simulations in Magnetic Resonance. An Object Oriented Programming Approach. J Magn. Res. 1994; 106a:75-105.

If you publish material that makes use of PyGAMMA, please cite the following publication:

Soher B, Semanchuk P, Todd D, Ji X, Deelchand D, Joers J, Oz G and Young K. Vespa: Integrated applications for RF pulse design, spectral simulation and MRS data analysis. Magn Reson Med. 2023;1-16. epub doi: 10.1002/mrm.29686

GAMMA was originally written by Scott A. Smith and Tilo Levante under the guideance of B.H. Meier and R.R. Ernst at the ETH in Zürich. It has since been modifed and updated with contributions from a number of individuals. The expansion of PyGAMMA using SWIG was accomplished as part of the [Vespa](https://github.com/vespa-mrs/vespa) project.	 

## Licensing

BSD, specifically a "three-clause" BSD license
