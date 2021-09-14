---
title: Installing Multicore Par2
---

If your device has more than 1 core available, you can significantly speed up verification and repair by using all cores in your system.
Installing these multicore versions of Par2 is easy for many platforms.

There are 2 versions available:

- `par2cmdline-tbb`: Based on Intel Thread Building blocks it is the fastest but can be harder (or impossible) to install on non-x86/x64 systems like ARM or older Ubuntu releases.
- `par2cmdline` **v0.7+** ([Github](https://github.com/Parchive/par2cmdline)): Easy to install on almost any platform, performance is better than single-threaded `par2` but less than `par2cmdline-tbb`.

After installation and restarting SABnzbd you can specify additional options, such as the maximum number of cores to use, in the `Extra PAR2 Parameters` setting.

This information does not apply to Windows or macOS, where Multicore par2 executables are included with SABnzbd distributions.


-------------------



## Installation on Ubuntu via PPA

For Ubuntu there is a PPA by the same creator (JCFP) as the SABnzbd PPA that has both versions.

Run these commands to install the PPA and `par2cmdline-tbb`:

```
sudo add-apt-repository ppa:jcfp/sab-addons
sudo apt-get update
sudo apt-get install par2-tbb
```

For `par2cmdline` change the last command to:

```
sudo apt-get install par2
```


-------------------



## Installation on other distributions



Tools required: `git`, `automake` and `make` (install via your distribution's package manager)

```
git clone https://github.com/Parchive/par2cmdline.git
cd par2cmdline
aclocal
automake --add-missing
autoconf
./configure
make
make install
```
<span class="label label-warning">NOTE</span> You might need to run the last command as `sudo` because it will install the `par2` command in the `bin` directory.

<span class="label label-warning">NOTE</span> Safest to uninstall your existing `par2` first!

After this, you can delete the `par2cmdline` folder.
