---
title: 🐾 How to setup Panthor on Mali GPUs with RK3588
description: 
published: true
date: 2025-09-13T08:53:13.718Z
tags: 
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# Enabling Panthor on Mali GPUs with RK3588 🚀

This guide walks you through the steps to enable Panthor and Vulkan on Mali GPUs present in boards with the RK3588 chipset.

# 🔧 Steps to Enable Panthor 

### 🎛️ 1. Enable the Panthor DTBO
#### 🤖 1.1 Automatically
The bredos-config tool offers a simple way to enable and disable dtbos. Start the tool with
```
sudo bredos-config
```
and navigate to `Device Tree Manager` -> `Enable / Disable Overlays` and enable `rockchip-rk3588-panthor-gpu`. The tool then installs the base device tree and the selected overlay. 

> Carefully follow the instructions on screen!
{.is-warning}

While bredos-config is able to install dtbs and alter the grub config to load them on boot it *cannot* alter uefi settings. This has to be done by the user. The changes the user has to made are shown by bredos-config on first installation of base/overlay dtbs. The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos).


#### 🦶 1.2 Manually
Follow the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos) to enable
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`

> Do not reboot your system after the installation of the dtb overlay!
{.is-warning}


### 🔄 2. Replace Panfork graphics

Replace the `mesa-panfork-git` package with the standard `mesa` package:

```  
sudo pacman -S mesa
```

### 🌋 3. Enable Vulkan

Install the vulkan loader and driver:
```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

### 🔁 4. Reboot Your System 
If you want to validate if your graphics, you can do run the following:
```
sudo pacman -S inxi mesa-utils
inxi -G
```