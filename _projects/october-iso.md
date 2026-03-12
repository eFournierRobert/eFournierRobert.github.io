---
layout: post
title: October ISO
tag: no_main_show
---

# October ISO
---
Github repository: [october-iso](https://github.com/october-os/october-iso)

---

It is good to have an installer, but installing an operating system will 
basically wipe the existing OS and replace it with the new one. You can 
see how wiping the OS that is executing the program that installs the new OS doesn't work.
It's a snake eating its own tail.
To solve this problem, we need to have an external bootable drive that the
computer can boot on and execute the installer on.

During the 1980s, people used floppy disk for this. One floppy disk would 
be bootable, then the installer would tell you to put another floppy in to
continue the installation, then another and then the next one until the
process of installing is done. Then, during the 1990s, this operation was done
from a CD-ROM and the 2000s replaced those with DVDs.

During this time, a file format was created which is called *Optical disc image* or ISO image.
An ISO file is, basically, a virtualized version of an optical drive file system.
This file is basically like another file and it can be passed around, put on other
drives etc. Operating systems quickly became able to use it just like any optical drives.

By the 2010s, this quickly became the standard way of distributing operating systems installation
media. You could make a bootable USB drive with an ISO file on it and then boot on it
easily just like you would with an optical drive. Since it is just a file, some tools
lets you have multiple ISOs simultaneously on a single drive.

Today, October Linux has its own ISO repository that can generate a fully working ISO file.
It contains both the installer and the list of packages that will be installed on top of a
basic Arch Linux installation.

## Generating an ISO

The repository contains a folder called archiso. This folder has an airootfs profile.
Airootfs lets us define files and folders just like it should be inside the ISO and it will
copy them over while generating an image. Basically, the folder `airootfs` is our profile 
root folder (`/`).

To generate a new ISO, we have a small script called `mkiso.sh`. When executed with no arguments,
it will create a development image. This image assumes you are executing it through a QEMU virtual 
machine and it will try to mount a folder on the host machine assumed to contain the code of the 
installer. When executed with the argument "release", it will create a release ISO containing 
the latest release of the installer.

The release script works in three steps:
1. It copies the package list from the documentation folder to `airootfs`.
2. Pulls the latest release of the installer, from Github, and puts the binary inside `/usr/bin` of 
  the `airootfs`.
3. It calls mkarchiso and gives it the profile on the repository so that it can generate an image 
  for us.

This is how we generate an ISO image of October Linux. Then, you can just flash a USB drive with it
using software like Ventoy or dd and you're good to go.
