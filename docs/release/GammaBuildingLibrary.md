---
sort: 6
---

# How to Build GAMMA

** These are older (almost deprecated) instructions for how to build GAMMA **.  See also the more recent documentation on [How to Build Wheels](PyGammaBuildingWheels.md).

This document tells you how to download GAMMA's source code build it on Linux, Windows, and OS X.

Please note that we have a separate page that describes [how to build PyGamma](PyGammaBuildingLibrary.md). This page is for GAMMA only.

## Download the Code

GAMMA's source code is stored in a [GitHub](http://github.com/) repository. If you do not have a Git installed on your computer, you will need to install it from  [here](https://git-for-windows.github.io/) for windows.  If you're on Lixux/MacOS it's likely already installed. On Windows you can also install an GUI based client, [TortoiseGit](http://tortoisegit.net/) is a popular one.

Once you have Git installed, open a Git command prompt, go to your development directory and enter the following command:
```
git clone https://github.com/pygamma-mrs/gamma.git
```

## Install a C++ Compiler

To build the libraries, you need a C++ compiler.

On Windows, the code works with [Visual Studio Express edition 2008](http://www.microsoft.com/visualstudio/en-us/products/2008-editions/express). Note that Visual Studio Express Edition 2008 cannot build 64-bit binaries. 

Under Linux use [GCC](http://gcc.gnu.org/). We've successfully built GAMMA using GCC 4.x. GCC 5.x might work too.

Under OS X, use Clang or GCC. 

You might want to consider installing an [optimized linear algebra library](../technical/performance/GammaWithBlasLapack.md) before building, although this is not essential and complicates the build a little.

## Install Python (Optionally, for Testing)

The tests use [Python](http://www.python.org/) as well as the Python libraries [numpy](http://numpy.scipy.org/) and [SciPy](http://www.scipy.org/). Many Linux systems have Python installed already, but be careful not to mess up your 'system' Python installation.

# Building GAMMA on Linux and OSX

Building is fairly straightforward. Start a command prompt and move to `gamma/platforms/Linux` or `gamma/platforms/OSX`.

The following commands are valid --

- _make all_  - This is the default target. It builds the shared and static libraries.
- _make so_ - Builds the shared library.
- _make lib_ - Builds the static library.
- _make install_ - Installs the shared and static libraries to `/usr/local/lib`, the GAMMA build utility to `/usr/local/bin`, and the header files to `/usr/local/include`.
- _make test_ - Runs the tests (requires Python).
- _make pysg_ - Builds [PyGamma PYGAMMA].
- _make pysgdist_ - Builds [PyGamma PYGAMMA] for distribution.

For the adventurous, we also have a document on [GammaStaticLinking statically linking GAMMA to BLAS]. 

### Installing and Using the gamma Command Line Utility

To install the GAMMA header files and the `gamma` build script on your system, use this command:
```
sudo make install
```

You can verify that it's installed properly by requesting the GAMMA version:
```
gamma -v
```

## Building Your Own Code that Uses GAMMA

Once you've run `make install`, you can compile your own code that uses GAMMA by including `gamma.h` in your code --

```
#include "gamma.h"
```

and running the gamma build command --

```
gamma -o output_file your_simulation_file.cc
```

Note that the gamma build utility is a BASH script and needs to be run under that shell.


# Building GAMMA on Windows

The GAMMA source provides two MSVC projects in the `gamma/platforms/msvc2008e` directory. The project for building the static library and tests is `static/gamma.sln` and `dynamic/gamma.sln` will build the dynamic library and [PyGamma PyGAMMA].

In Windows Explorer, double click on the `.sln` file that contains the project you want to build. Hit F7 to build the whole project, or open the Solution Explorer (via the View/Solution Explorer menu item) if you only want to build individual items.

The static build creates the file `gamma/i686-pc-msvc/gamma.lib`. The dynamic build also puts its output in `gamma/i686-pc-msvc`. 

## Building Your Own Visual Studio Project that Uses GAMMA

To set up an MSVC project to build with the GAMMA libraries, make the following changes to your MSVC project under the "Configuration Properties" --

  * C/C++/General: set _Additional Include Directories_ to `..\..\src`
  * C/C++/Code Generation: set _Runtime Library_ to _Multi-Threaded (/MT)_ for use with the static library.
  * Linker/General: set _Additional Library Directories_ to `..\..\i686-pc-msvc`
  * Linker/Input: set _Additional Dependencies_ to `gamma.lib`
  * Linker/General: set _Output File_ to `..\..\i686-pc-msvc\your_output_file.exe`

Note these settings will need to be set for "All Configurations" or for Release and Debug independently.

A sample project that links to the static library is located in the `gamma/msvc2008e/fid_test`.