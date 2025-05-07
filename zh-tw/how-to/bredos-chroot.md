---
title: BredOS-Chroot utility
description: A simple tool to mount and chroot into a BredOS install from a secondary system
published: true
date: 2025-05-07T17:48:24.068Z
tags: null
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

Available as part of the `bredos-tools` package.

## Usage

```
Usage: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Example:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Mounts the given Btrfs partition with subvolumes and the boot partition,
then chroots into the system. Cleans up after exiting chroot.
```

Assuming you have a SDCard of a failed system, visible from `lsblk` at /dev/sdb, you can just run:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

And you would get a root shell into the broken system, facilitating repair.

Once repair is complete, you can just close the shell by typing `exit` or Ctrl + D, and the attached card would be unmounted.