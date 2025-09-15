---
title: BredOS-Chroot utility
description: セカンダリシステムからBredOSインストールにマウントしてクロートする簡単なツール
published: true
date: 2025-09-15T06:05:42.545Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. インストール

`bredos-tools`パッケージの一部として利用できます。 デフォルトでは、これをインストールする必要があります。 インストールされていない場合

```
sudo pacman -S bredos-tools
```

## 2. 使用法

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