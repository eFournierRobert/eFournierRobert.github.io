---
layout: post
title: Typewriter OS
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    Simple, Linux based embedded x86_64 OS
</div>
<!--excerpt-end-->

# Typewriter OS
---
Codeberg Repo : [typewriter-os](https://codeberg.org/efournierrobert/typewriter-os)

OS user space: [Modern operating systems](/2026/08/12/modern-os.html)

---

Typewriter OS is a small, purpose-built CLI x86_64 operating system based on Linux 7.1.7. It has a fully custom user space written in Rust.

{% include image.md image-url="/typi/typi-screenshot.png" %}

## Core idea
The idea behind this OS was to make it for an embedded device that would act as some sort of typewriter. 
The user space has all the core utilities needed for file managements, a [text editor](https://github.com/AchroDev/TuiText) and shell to navigate the file system.

The user is jailed inside the home directory `/home/writer/` so all their files can be stored persistently.

## Structure

This OS was made to be closer to an embedded device OS rather than a desktop Linux. The production build script generates a file called `typewriter.img` which 
stores both the persistent storage the core system storage.

The image is built to work with UEFI firmware so it contains two partitions:
- boot partition
- user storage partition

The boot partition is a `vfat` partition containing the kernel and the `initramfs` image made for the OS while the user storage partition is just a persistent data
partition formatted in `ext4`.

The `initramfs` contains the whole filesystem and the programs binaries. This allows us to replace the file in case of a system update and to have an unmodifiable core
that won't break if the user breaks free of the jail and removes system files. If this happens, the user can just reboot and the system will come back to a working
state.

## Programs

Typewriter OS has a small list of programs to let users accomplish their tasks. This includes core programs like:
- init - A custom made init system
- [TuiText by AchroDev](https://github.com/AchroDev/TuiText) - TUI text editor
- CLI shell - A minimal CLI shell

It also contains a list of core utilities to interact with the filesystem:
- copy - Copying files and directories
- create - Create new directories
- delete - Delete a file or a directory
- fetch - See system information
- find - Find a file in a given directory
- list - List the content of a directory
- move - Move a file or a directory
- new - Create a new file
- rename - Rename a file or a directory
- search - Search a specific substring in a file
- show - Show the content of a file