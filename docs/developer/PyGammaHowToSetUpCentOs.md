---
sort: 2
---

# Linux Setup - CentOS 7

This document describes how I set up CentOS 7 to build Linux PyGamma wheels. I used CentOS as a VirtualBox guest.

If you want to build 64-bit PyGamma wheels, you need 64-bit CentOS. As of 2019 we are no longer supporting 32-bit PyGAMMA builds.

## Support

PEP 599 identifies CentOS 7 as the benchmark system on which a wheel should work for it to be broadly compatible. Since 2019 we (PyGAMMA) have followed PEP 599 and the ‘manylinux2014' rules that user compilation under CentOS 7. To try to build wheels that are as widely usable as possible.

CentOS 7 will be supported (albeit only with critical security updates) until 2024 according to the CentOS FAQ: https://wiki.centos.org/FAQ/General.

## Installation in VirtualBox

I downloaded the CentOS7 ISO 'CentOS-7-x86_64-DVD-1908.iso' and created a new VirtualBox VM. 

In VirtualBox, File->NewMachine. Enter a name, select Red Hat and 64bit. Next, give it >= 4Gb RAM. Next, create a VDI format hard drive. Next, make it dynamically mounted. Next, set max hard drive to 500GB. Hit Create.

Select that VM from the list. Open settings. Under Storage, click on empty CDRom. Mount the CentOS7 ISO image to the CD. Under Display, set the video memory a bit larger (64Mb), make sure Graphics Controller is VMSVGA (for bigger screen?). 

Boot the machine. On first screen, select 'Install CentOS7'.  Eventually, the installer wizard will fill the screen.

Installation wizard. Select English. Next screen is Installation Summary. Set Date and Time if needed. 

Click Software Selection. Make Base Environment 'GNOME Desktop'. For Add-Ons:  'Development tools' and 'SysAdmin' and 'GNOME Applications'. Click Done. 
  
Installer wizard also wanted me to set up Installation Destination (it had the orange warning icon) so I clicked on it and then on Done because the defaults were fine. 

I then clicked on Begin Installation. 

The install moved on to the Create User page. Set up a root passwd. Click Done. Set up user name and passwd. Save these somewhere safe.  I made bsoher administrator just for kicks, also it seems to allow me sudo rights after I logged in.  Clicked on Done. 

The install 'thought' for a while (5-10 min) installing ~1500 packages and then about 'Performing post-installation setup tasks'. It finally said 'Complete' and offered a 'Reboot' button. I hit the Reboot button.

## First Reboot

Ended up in another wizard - Initial Setup

Clicked on Licesnse Information.  Accepted the license, clicked Done.

Click FInish Configureation, and it rebooted.

## First Login

It offered to log me (Brian Soher - user created during install) in.  There were a few GUI setup bits. Then a Getting Started ran.  I closed it.

Ran a Terminal. Typed >gcc -v  and  >swig -version.  I found that gcc and gcc-c++ were already installed (v 4.8.5), swig was installed but way earlier version (v 2.0.10). I used NAT to attach the network, but had to enable wired network in the Power drop menu (top right). 

On the first reboot after installation was complete, CentOS will update itself with the latest patches.

Next, you'll want to install VirtualBox guest additions to make the guest OS easier to use. In order to do that, you first have to add yourself to the `sudoers` file.

## (deprecated) Adding Yourself to sudoers

This section may not be needed if you set up your user account to be Administrator. I leave it here in case you didn't

Likely you will need to login as root to do this.

1. `su -`
1. `vim /etc/sudoers`
1. At the end of the file, add this line:
 your_username      ALL=(ALL)    ALL
1. Save the file with `:wq!`
1. Type `exit` to exit the `su -` shell.

## Building VirtualBox Guest Additions

Next few steps from: https://itekblog.com/centos-7-virtualbox-guest-additions-installation-centos-minimal/

>su root (enter passwd)

>yum update             (could be 1000+ packages to update)
>reboot

>yum update kernel      (may be done already by previous step)
>reboot

>yum install kernel-devel

From the Virtual Box -> Devices menu, select Insert Guest Additions CD Image. The CD icon will appear and you will be asked if you want to AutoRun the install process.  Click yes, and wait a bit.  You should see things being 'built' and installed.  Need to reboot for changes to take effect (I think).

## Create Shared Folder to Host to CentOS7

Poweroff the CentOS7 machine.  In VirtualBox Settings, Shared Folders, add new folder.  I told it to grab 'D:\users\bsoher', auto mount it, and mount it at '/home/bsoher/sf_bsoher'. And close.  

Restart CentOS7 machine.

You should see the new folder, but have limited permissions to access (as in non-stop typing of my admn passwd). So do this.

Run a Terminal.  

>sudo usermod -aG vboxsf bsoher

Restart the CentOS7 machine. And now I can cruise around that directory with no problems.

## Adding Packages

Switch to root for this. Make sure internet connected. Check that these packages are installed: `xz zlib zlib-devel openssl-devel pcre-devel sqlite-devel`. I did it using:

>rpm -qa | grep <pkg-name>

and found only xz and zlib installed.  So, I did the following:

>yum install xz zlib zlib-devel openssl-devel pcre-devel sqlite-devel

## Building Python

CentOS 7 comes with Python 2.7. To use a newer Python, I used the Miniconda installer script. Based on some vague advice from Google I downloded Miniconda2 since CentOS 7 system Python is 2.7.5.  I used the 'conda' command to set up a python 3.7 environment.

## Download and Install pip

Pip comes with Miniconda and Python 3.7 environment as does setuptools and wheel, both of which we need.

## Download and Build SWIG

1. Download and untar the SWIG source code. I was able to use the latest (4.0.2 as of this writing).
1. Build with `sudo ./configure && sudo make && sudo make install`

----


## CentOS 5.11 Setup

**Deprecated Deprecated Deprecated Deprecated Deprecated Deprecated**

The following instructions are included here for historical jocularity. Steps to set up CentOS 7 as a VM are given above and should be used to create Python 3 wheels.

This document describes how I set up CentOS 5.11 to build Linux PyGamma wheels. I used CentOS as a VirtualBox guest.

This document makes no distinction between 32- and 64-bit Linux. The instructions are the same for each. If you want to build 32-bit PyGamma wheels, you need 32-bit CentOS. If you want to build 64-bit PyGamma wheels, you need 64-bit CentOS. It's probably possible to build 32-bit binaries on the 64-bit platform, but I haven't worked out how.

### Support

CentOS 5.x will be supported (albeit only with critical security updates) until 31 March, 2017 according to the CentOS FAQ: https://wiki.centos.org/FAQ/General.

### Installation

I downloaded the ISO and installed as one normally does under VirtualBox. During the installation, I opted to disable SELinux.

### Post-Install Configuration

On the first reboot after installation was complete, CentOS will update itself with the latest patches.

Next, you'll want to install VirtualBox guest additions to make the guest OS easier to use. In order to do that, you first have to add yourself to the `sudoers` file.

#### Adding Yourself to sudoers

1. `su -`
1. `vim /etc/sudoers`
1. At the end of the file, add this line:
 your_username      ALL=(ALL)    ALL
1. Save the file with `:wq!`
1. Type `exit` to exit the `su -` shell.

#### Building VirtualBox Guest Additions

First, install GCC --
```
sudo yum install gcc gcc-c++ 
```

Next --
1. Insert the Guest Additions CD. (The Guest Additions are an ISO file that you download from VirtualBox.org. I think they're provided under a different license than the main program which is why you have to download them separately.)
1. Start a terminal and `cd /media/VBOXADDITIONS_xxxx`. Note that the exact name of the `VBOXADDITIONS` directory changes with each each version of VirtualBox.
1. sudo ./VBoxLinuxAdditions.run
1. Eject the Guest Additions CD and reboot.

#### Adding Packages

Install the things you'll need to build Python and swig, and to use pip --

```
sudo yum install xz zlib zlib-devel openssl-devel pcre-devel sqlite-devel
```

#### Building Python

CentOS 5.11 comes with Python 2.4. To use a newer Python, download and untar the source code for the Python you want to use and then build it. For the Python 2.7.11 source that I used, I built with these steps --
```
sudo ./configure --enable-unicode=ucs4
sudo make altinstall
```

Using UCS4 (as opposed to the default UCS2) during the configure step is important. See here for details:
https://www.python.org/dev/peps/pep-0513/#ucs-2-vs-ucs-4-builds

`make altinstall` tells Python to install itself in such a way that it doesn't interfere with the default (system) Python.

Once my Python was built, I added a symlink to make it the default Python in my shell --
```
sudo ln -s /usr/local/bin/python2.7 /usr/local/bin/python
```

At this point, if you start a new terminal and type `python`, you should get Python 2.7.11.

#### Download and Install pip

1. `wget --no-check-certificate https://bootstrap.pypa.io/get-pip.py`
1. sudo python get-pip.py

This also installs setuptools and wheel, both of which we need.

#### Fix pip

`pip` gets a little confused when installed in this context. Its 3 scripts contain an incorrect shebang line. (See
[pip issue 1918](https://github.com/pypa/pip/issues/1918) for more details.)
Use `sudo vim` to edit these 3 scripts --
 * `/usr/local/bin/pip`
 * `/usr/local/bin/pip2`
 * `/usr/local/bin/pip2.7`

In each, change the first line from this --
```
#!/usr/bin/python
```
to this --
```
#!/usr/local/bin/python
```


#### Download and Build SWIG
1. Download and untar the SWIG source code. I was able to use the latest (3.0.8 as of this writing).
1. Build with `sudo ./configure && sudo make && sudo make install`