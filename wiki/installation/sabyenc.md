---
title: SABYenc 3
redirect_from:
    - /sabyenc
    - /wiki/extra/sabyenc.html
---

# Introduction to SAByenc

In SABnzbd 3.0.0 we introduced a new module called `sabyenc3` to increase the download speed on CPU-limited devices. `sabyenc3` takes care of decoding yencoded articles on usenet.

With SABnzbd 3.6.0, we introduced version 5.0.0 of sabyenc3 which uses SIMD ("Single instruction, multiple data", a type of parallel processing by the CPU) on x86 and ARM processors, which speeds up yenc decoding with a factor 5 to 10.

The Windows- and macOS-packages of SABnzbd automatically contain that module. On other platforms (like Linux and FreeBSD) you have to make sure the module is installed. The information below is for packagers and source code users on those platforms.

### Version dependency

SABnzbd 3.5.x and lower only works with `sabyenc3` version 4.0.x

SABnzbd 3.6.x and higher only works with `sabyenc3` version 5.0.x

If SABnzbd detects the wrong version of `sabyenc3`, it will print out an error message.
    
# Installation with Python's packaging manager `pip` 

<div class="alert alert-warning">
    These instructions assume that <code>python</code> and <code>pip</code> refer to the Python 3 installation on your system.<br>On some older systems Python 2 is the default <code>python</code> and you should instead use the <code>python3</code> and <code>pip3</code> commands.
</div>

<hr/>

Inside the source directory of SABnzbd, run this command

```
pip install -r requirements.txt
```

It will take care of installing the right version of `sabyenc3`. This will work for x86 and ARM.

You might need to first install the python-development module (`python3-dev` or `python3-devel`), and then run the above `pip` command.

If you need to install a specific version to match your version of SABnzbd, you can specify this in the command:

```
pip install sabyenc3==4.0.2
```

<hr/>


# Installation on Linux

**Jump to: [Ubuntu (via PPA)](#installation-on-ubuntu-via-ppa), [Ubuntu](#installation-on-ubuntu-without-ppa), [Fedora / RedHat](#installation-on-fedora--redhat), [OpenSuSE](#installation-on-opensuse) or [FreeBSD](#installation-on-freebsd).**

### Installation on Ubuntu via PPA

For Ubuntu there is a PPA with `python-sabyenc`, by the same creator (JCFP) as the SABnzbd PPA. This will work on X86, X86-64, ARM (32bit) and ARM64 architectures.
Install it like this:
```
sudo add-apt-repository ppa:jcfp/sab-addons
sudo apt-get update
sudo apt-get install python-sabyenc
```

### Installation on Ubuntu (without PPA)

Short method, only works on X86 and X86-64
```
sudo apt-get install python3-pip
sudo -H pip install sabyenc3 --upgrade
```

Long, with your own compiling:
```
sudo apt-get install python3-dev python3-pip
sudo -H pip install sabyenc3 --upgrade
```

### Installation on Fedora / RedHat

Short method, only works on X86 and X86-64

All as root:
```
pip install --upgrade pip
pip install sabyenc3 --upgrade
```

Long, with your own compiling:

```
yum install -y python-devel gcc redhat-rpm-config
pip install --upgrade pip
pip install sabyenc3 --upgrade
```

### Installation on OpenSuSE
All as root

Short, works on X86 and X86-64
```
zypper install -y python-pip
pip install --upgrade pip
pip install sabyenc3 --upgrade
```

Long, with your own compiling:

```
zypper install -y python-pip python-devel gcc
pip install --upgrade pip
pip install sabyenc3 --upgrade
```

<hr/>

## Multiple installations of python

If you have multiple installations of Python on your machine (<code>python</code>/<code>python2</code>/<code>python3</code> or different versions of Python 3), you have to make sure SAByenc is installed into the correct Python enviroment. And 'correct' means the Python installation used by SABnzbd. The command is then:

```
/path/to/correct/python -m pip install sabyenc3
```

## Check if SABYenc is correctly installed

To check if SABYenc is correctly installed, run this Python oneliner:
```
python -c "import sabyenc3; print(sabyenc3.__version__, sabyenc3.__file__);"
```
It should print the version of the installed `sabyenc3` module, without any errors.


## SABnzbd's Checking & Logging

SABnzbd will check if SAByenc is installed.
If SAByenc is installed, and the version is correct, SABnzbd will print in the log:

```
SABYenc module (v4.0.2)... found!
```

If your version of `sabyenc3` does not match the version required by SABnzbd, you get:
```
SABYenc disabled: no correct version found! (Found v4.0.2, expecting v5.0.1)
```

If you have no `sabyenc3` module installed, or an incorrect version (too low or too high (!)), you will get a warning:

```
SABYenc module... NOT found! Expecting v4.0.2
```

## Issues

If you experience any issues, please let us know on our [Forums](https://forums.sabnzbd.org/) or [Github](https://github.com/sabnzbd/sabnzbd/issues)!
