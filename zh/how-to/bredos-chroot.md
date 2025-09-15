---
title: BredOS-Chroot 实用程序
description: 一个从二级系统挂载到 BredOS 安装的简单工具
published: true
date: 2025-09-15T06:05:42.545Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. 安装

可用作 `bredos-tools` 软件包的一部分。 默认情况下应该安装。 如果不安装它

```
sudo pacman -S bredos-tools
```

## 2. 用法

Run `bredos-chroot` without any parameters to display the help message.

```
用法：/usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

示例：
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

挂载给定的 Btrfs 分区与子卷和引导分区，
然后在系统中 chroot。退出 chroot 后清理。
```

## 3. Example

Assuming you have a SDCard of a failed system, visible from `lsblk` at **/dev/sdb**, you can just run:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

While `/dev/sdb3` is your BredOS root partition and `/dev/sdb2` is your BredOS boot partition.

This will get a root shell into the broken system, facilitating repair.

Once repair is complete, you can just close the shell by typing `exit` or Ctrl + D, and the attached filesystem would be unmounted.