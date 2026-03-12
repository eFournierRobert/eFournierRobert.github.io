---
layout: post
title: Octoberctl
tag: no_main_show
---

# Octoberctl
---
Github repository: [octoberctl](https://github.com/october-os/octoberctl)

AUR: [octoberctl-bin](https://aur.archlinux.org/packages/octoberctl-bin)

---

The configuration of October Linux isn't a one and done deal. Over time, it is being
updated with new features and bug fixes. Also, we wanted to provide an easy
way to do simple things, like adding a wallpaper, without always 
having to dig into the configuration folders.

This is why we created and introduced octoberctl to the distribution.
It is a CLI tool, written in the Go programming language, that manages the 
configuration. It was also published to the AUR for easy updates with yay.

## Updating

This tool helps with updating the configuration to the latest changes in the
Github repository. It basically does a `git fetch` and then `git reset --hard`
on the main branch to pull them. They'll be applied automatically.

If octoberctl detects any changes to the core configuration, it will ask 
you to "force" an update. This is a safe guard so you don't override wrongly
placed custom changes while trying to update.

## Wallpapers

It can also manage the `wallpapers` folder for you. Always copying or moving files
around to this folder wasn't the right flow, so octoberctl does all this for you.
You can do the following actions for wallpaper management:

- list (-l) -- List all the wallpapers in the folder. Also indicates which is the current one.
- show (-s) -- Shows a given wallpaper in the terminal.
- add (-a) -- Adds a wallpaper to `wallpapers`.
- remove (-r) -- Removes a wallpaper from `wallpapers`.
