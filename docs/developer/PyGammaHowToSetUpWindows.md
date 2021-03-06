---
sort: 1
---

# Windows Setup

We need to compile Gamma and PyGamma with the [same compiler used to compile the CPython](../technical/pygamma/WhatCompilerIsMyPython.md) on which we intend to import PyGAMMA/GAMMA. For Python 3.7 it is Visual Studio 2017. For Python 2.7 it was Visual Studio 2008. We no longer officially support Python 2.7, so the next section will only go over how we build and test for Python 3. And as of this writing, we've only tested for Python 3.7, but I'm sure there will be more to come eventually.

## Setting up Windows Build environment

Install Visual Studio 2019 Community edition, which is free. While on the Installer dialog's configuration page (where you can pick what it installs), select the "Desktop development with C++" module from the icons in the left column. Then on the right column, you can select more/less options within that module. Be sure to select the "Windows 10 SDK" and "MSVC v141 - VS 2017 C++ x64/x86 build tools". *This will allow you to compile Gamma using the VS 2017 compiler within the VS 2019 IDE*.

The gamma.sln files in either the msvc2017\dynamic or msvc2017\static should open up within VS 2019 after it installs with all the appropriate settings already selected. I usually right click on the gamma.sln entry in the Solution Explorer and select "Build Solution" to create the library, but that's just me.  This isn't a tutorial on VS 2019.

There are two other programs needed to perform a Build. SWIG has to be installed. For Python 3.x we have been using version 4.0.1. The SWIG executable should be discoverable on your PATH environment variable.  There are also some calls to Python scripts, so Python has to be discoverable on your PATH environment variable. 

**NB. the first Python install found in your Windows PATH is the one that will be used for all steps in the Build.**  So if you have multiple Python installtions (e.g. 3.5, 3.6, 3.7 etc) make sure that the first one in PATH is the one against which you want to compile PyGamma.  I usually do this in the Windows Environmental Variable dialog where I edit PATH and just 'move up' the Python paths that I want to the top of the list. I can then change it back afterwards if necessary.

## Static and Dynamic libraries and Where is PyGamma?

Honestly, our true fixation is creating PyGamma, which uses the DLL created in the 'dynamic' project. However, Gamma is easier to test if it is statically linked to the test programs. So we have the two different solutions 'static' and 'dynamic' which allow us to do both things.  

The static project has nothing to do with PyGamma, just for testing that Gamma (and any changes we have made to Gamma) is working. And honestly, it only tests the things in the various test programs we have. So, if you add any code to the Gamma library and want to test it, you should consider extending these tests which live in `gamma\src\Tests`.

The dynamic project is where PyGamma actually gets created and compiled with Gamma.  There is a step in building the solution where the SWIG program (needs to be in your PATH environmental variable) is run that creates the python.py and pygamma_wrap.cxx source files.  The pygamma_wrap.cxx file is compiled as part of the DLL that the dynamic project outputs (as a file named _pygamma.pyd) and the pygamma.py module contains the Python source code to access the objects in the DLL.

In both the static and dynamic projects, there are Pre- and Post-Build Events (seen in Properties->Build Events->Pre-Build Event, etc.) that help move things along. Like making sure that the 'i686-pc-msvc' directory exists at the top level directory of the gamma hierarchy. And running various Python scripts like write_python_include_path.py, python copy_python_lib.py and post_build.py, that do all sorts of useful moving, copying and creating actions before and after the Build.

In the case of the static project, the Post-Build Event in the 'static\test' sub-project actually automatically triggers the run_tests.py script that we use to confirm the functionality of the Build. It reports test results in the VS 2019 Console window.

For the dynamic project (and subsequent creation of the pygamma module) tests cannot be automatically run because a pygamma wheel has to be created and installed in Python.  Since there may be multiple Python installations, we let the user manually perform these steps. This is generally done using a command line window, changing to the gamma\pygamma directory and running `python setup.py bdist_wheel` command which will create the wheel in the 'dist' subdirectory. Change to the dist directory, run 'pip uninstall pygamma' command to remove any existing version (important if you are not changing the version number) then run `pip install <wheel name>` to install the new pygamma library.  Remember, this will install pygamma into whatever Python installation is 'active' in your command window. I recommend that you use something like the 'miniconda' package manager to organize your different Python environments. Then you can just activate whichever one you want to use to test your new library.

