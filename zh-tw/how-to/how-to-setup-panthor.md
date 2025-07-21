---
title: 🐾 How to setup Panthor on Mali GPUs with RK3588
description:
published: true
date: 2024-11-10T19:29:32.381Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# Enabling Panthor on Mali GPUs with RK3588 🚀

This guide walks you through the steps to enable Panthor on Mali GPUs present in boards with the RK3588 chipset.

# 🔧 Steps to Enable Panthor

### 🎛️ 1. Enable the Panthor DTBO

Follow the [Device Tree Overlay guide]/how-to/how-to-enable-dtbos) to enable
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**Do not reboot your system after copying the DTBO!**

### 🔄 2. Replace Panfork graphics

Replace the `mesa-panfork-git` package with the standard `mesa` package:

```
sudo pacman -S mesa
```

### 🔁 3. Reboot Your System

If you want to validate if your graphics, you can do run the following:

```
sudo pacman -S inxi mesa-utils
inxi -G
```