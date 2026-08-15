---
layout: post
title: Typewriter OS
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    Simple, Linux-based embedded x86_64 OS
</div>
<!--excerpt-end-->

# Typewriter OS
---
Codeberg Repository : [typewriter-os](https://codeberg.org/efournierrobert/typewriter-os)

Related article: [Modern operating systems](/2026/08/12/modern-os.html)

---

Typewriter OS is a small, purpose-built CLI x86_64 operating system based on Linux 7.1.7. It has a fully custom user space written in Rust.

{% include image.md image-url="/typi/typi-screenshot.png" %}

## Core idea
The idea behind this OS was to make it for an embedded device that would act as some sort of typewriter. 
The user space has all the core utilities needed for file management, a [text editor](https://github.com/AchroDev/TuiText) and shell to navigate the file system.

The user is confined inside the home directory, `/home/writer/`, where all their files are stored persistently.

## Structure

This OS was made to be closer to an embedded device OS rather than a desktop Linux. The production build script generates a file called `typewriter.img` which 
stores both the persistent user storage the system storage.

The image is designed to boot using UEFI firmware and contains two partitions:

- a boot partition;
- a user-storage partition.

The boot partition is a `vfat` partition containing the kernel and the `initramfs` image made for the OS while the user storage partition is a persistent data
partition formatted with `ext4`.

The `initramfs` contains the core filesystem and the programs binaries. This makes system updates simple. The `initramfs` can be replaced as a single file.
It also keeps the core system intact, so changes to system files don't permanently break the installation.

## Programs

Typewriter OS has a small set of programs to let users accomplish their tasks. This includes core programs like:

- init - A custom-made init system
- [TuiText by AchroDev](https://github.com/AchroDev/TuiText) - TUI text editor
- CLI shell - A minimal CLI shell

It also contains a small set of core utilities to interact with the filesystem:

- copy - Copying files and directories
- create - Create new directories
- delete - Delete a file or a directory
- fetch - See system information
- find - Find a file in a given directory
- list - List the contents of a directory
- move - Move a file or a directory
- new - Create a new file
- rename - Rename a file or a directory
- search - Search for a specific substring in a file
- show - Show the content of a file