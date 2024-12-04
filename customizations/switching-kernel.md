---
title: Switching Kernel
description: 
published: false
date: 2024-12-04T16:14:22.945Z
tags: 
editor: markdown
dateCreated: 2024-12-04T15:50:46.861Z
---

# Installing a different kernel
By default, most devices ship with the `linux-rockchip-rkr3` kernel.
However you may wanna switch from another, or to another kernel.
To do this first please validate which kernel you have installed:

```
pacman -Qs linux | grep "linux"
```

This will output a list, like:

```
[bill88t@duo | ~]> yay -Qs linux | grep "linux"
local/archlinux-keyring 20241203-1
local/archlinuxarm-keyring 20240419-1 (base-devel)
local/cpupower 6.12-1 (linux-tools)
    Userspace utilities for linux-erofs file system
    A key remapping daemon for linux
local/lib32-util-linux 2.40.2-1
local/linux-api-headers 6.10-1
local/linux-firmware 20241111.b5885ec5-1
local/linux-firmware-whence 20241111.b5885ec5-1
local/linux-rockchip-rkr3 2:6.1.75-17
local/linux-rockchip-rkr3-headers 2:6.1.75-17
local/util-linux 2.40.2-1
local/util-linux-libs 2.40.2-1
    util-linux runtime libraries
```

In the list we can see linux-rockchip-rkr3 and the accompanying headers are installed.
To install a different kernel, first remove the installed kernel, along with it's headers.

## 1. Remove the installed kernel
```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

From this point on it's NOT SAFE TO REBOOT.

## 2. Proceed to install the new kernel

```
sudo pacman -S your-new-kernel your-new-kernel-headers
```

The kernel package will generate an initramfs image. You can find it's filename from the install log:

```

```