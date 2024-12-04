---
title: 切换内核中
description: null
published: false
date: 2024-12-04T16:21:13.994Z
tags: null
editor: markdown
dateCreated: 2024-12-04T15：50：46.861Z
---

# 安装另一个内核中

默认情况下，大多数设备都使用 `linux-rockchip-rkr3` 内核。
然而，您可以从另一个开关，或者到另一个内核。
要做到这一点，请首先验证您已经安装了哪些内核：

```
pacman -Qs linux | grep "linux"
```

这将输出一个列表，如：

```
[bill88t@duo | ~]> yay -Qs linux | grep "linux"
local/archlinux-key环20241203-1
local/archlinuxarm-key环20240419-1 (base-devel)
local/cpupower 6. 2-1 (linux-tools)
    Linux-erofs 文件系统的用户空间工具
    Linux
local/lib32-util-Linux 2.40 -1
local/linux-api-headers 6.10-1
local/linux-firmware 202411.b5885ec5-1
local/linux-firmware-whence 202411.b5885ec5-1
local/linux-rockchip-rkr3 2:6. .75-17
local/linux-rockchip-rkr3-headers 2:6.1.75-17
local/util-Linux 2.40.2-1
local/util-linux-libs 240.2-1
    util-Linux runtime 库
```

在列表中，我们可以看到linux-rockchip-rkr3和配对的头已安装。
要安装另一个内核，请先移除已安装的内核及其头部。

## 1. 删除已安装的内核。

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

从这一点开始，它不会保存到REBOOT。

## 2. 继续安装新内核。

```
sudo pacman -S your new-kernel headers
```

内核包将生成一个 initramfs 图像。 您可以从安装日志中找到它的文件名：

```
(14/30) Updating linux initcpios...
==> Building image from preset: /etc/mkinitcpio.d/linux-rockchip-rkr3.preset: 'default'
==> Using configuration file: '/etc/mkinitcpio.conf'
  -> -k /boot/vmlinuz-linux-rockchip-rkr3 -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-rockchip-rkr3.img
==> Starting build: '6.1.75-rkr3'
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [autodetect]
  -> Running build hook: [modconf]
  -> Running build hook: [kms]
  -> Running build hook: [keyboard]
  -> Running build hook: [keymap]
  -> Running build hook: [consolefont]
==> WARNING: consolefont: no font found in configuration
  -> Running build hook: [block]
  -> Running build hook: [filesystems]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating zstd-compressed initcpio image: '/boot/initramfs-linux-rockchip-rkr3.img'
==> Initcpio image generation successful
```
