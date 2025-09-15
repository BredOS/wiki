---
title: BredOS-Chroot utility
description: A simple tool to mount and chroot into a BredOS install from a secondary system
published: true
date: 2025-09-15T06:05:42.545Z
tags: 
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. Installation

Available as part of the `bredos-tools` package. By default this should be installed. If not install it with
```
sudo pacman -S bredos-tools
```

## 2. Usage
Run `bredos-chroot` without any parameters to display the help message.

```
Usage: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Example:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Mounts the given Btrfs partition with subvolumes and the boot partition,
then chroots into the system. Cleans up after exiting chroot.
```

## 3. Example

Assuming you have a SDCard of a failed system, visible from `lsblk` at **/dev/sdb**, you can just run:
```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

While `/dev/sdb3` is your BredOS root partition and `/dev/sdb2` is your BredOS boot partition.

This will get a root shell into the broken system, facilitating repair.

Once repair is complete, you can just close the shell by typing `exit` or Ctrl + D, and the attached filesystem would be unmounted.