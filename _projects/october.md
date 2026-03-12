---
layout: post
title: October Linux
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    Arch based Linux distribution.
</div>
<!--excerpt-end-->

# October Linux
---
Co-creator and co-maintainer: [Arianne](https://arianne.dev)

Github Organization: [October Linux](https://github.com/october-os)

---
October Linux is a Linux distribution that I co-created and co-maintain. We wanted to offer a 
distribution that kept the simplicity of Arch Linux, but built on top of it to offer a more complete experience.
It is in continuous development so we keep adding new features and correcting bugs over time.

## Subprojects
Building a distribution is a big project, so we divided it into four subprojects that each serve 
a function in the operating system.

The four subprojects are listed bellow.

### October installer

October installer is the installer for the operating system. Arch famously has a command line 
install process and, only recently, did they started offering archinstall as an alternative. 
For our distribution, we wanted to offer a complete and painless install process where you 
only need to submit a configuration and the installer takes care of the rest for you.

[Learn more about October installer.](/projects/october-installer)

### October ISO

To install the operating system we needed an ISO. This is the project with everything needed
to build a functional and bootable ISO that can install October Linux.

[Learn more about October ISO.](/projects/october-iso)

### October config

October needed a configuration and this is the project containing it. By configuration,
we mean fully working configurations for Hyprland, Quickshell and etc. All integrated as
a single beautiful and usable unit.

[Learn more about October config.](/projects/october-config)

### Octoberctl

We didn't want the users to manage the configuration by themselves, so we built a small
command line utility tool that manages it for you. It can update the configuration to 
the latest changes available and manage the wallpapers you currently have.

[Learn more about Octoberctl.]()
