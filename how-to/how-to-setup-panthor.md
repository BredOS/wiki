---
title: Setup Panthor on Mali GPUs with RK3588
description: 
published: true
date: 2026-01-20T10:04:59.437Z
tags: 
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 1. Introduction

This guide walks you through the steps to enable Panthor and Vulkan on Mali GPUs present in boards with the RK3588 chipset.

## 1.1 Whats the difference between Panthor and Panfork?
Panthor is a new driver for Mali G*** gpus developed by the linux kernel developers, while Panfork is a fork from Panfrost which aimed to support Mali G610 when it was released. Even so Panfork performs better than Panthor, Panthor is the way to go forward as Panfork isnt supported anymore.

 - Overview about performance on Panthor:
```
> EGL (2D acceleration) performance ~-40% (not measured, answering from day to day feel).
> OpenGL (3D acceleration) performance -16%.
> Vulkan is now almost fully supported.
> You also see a bit more cpu usage (~5%) on heavy gpu usage.
```

> BredOS for RK35xx devices has Panfork enabled by default!
{.is-info}

# 2. Install Panthor
## 2.1 Enable the DTBO
### 2.1.1 Automatically
- The bredos-config tool offers a simple way to enable and disable dtbos. Start the tool with:
```
sudo bredos-config
```
Then navigate to `Device Tree Manager` -> `Enable / Disable Overlays` and enable `rockchip-rk3588-panthor-gpu`. The tool then installs the base device tree and the selected overlay. 

> Carefully follow the instructions on screen!
{.is-warning}

While bredos-config is able to install dtbs and alter the grub config to load them on boot it *cannot* alter uefi settings. This has to be done by the user. The changes the user has to make are shown by bredos-config on first installation of base/overlay dtbs. The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos).


> Do not reboot your system after the installation of the dtb overlay!
> Continue with `2.2 Replace Panfork graphics`.
{.is-warning}
### 2.1.2 Manually
Follow the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos) to enable `/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`.

> Do not reboot your system after the installation of the dtb overlay!
> Continue with `2.2 Replace Panfork graphics`.
{.is-warning}


## 2.2 Replace Panfork graphics

- Replace the `mesa-panfork-git` package with the standard `mesa` package:

```  
sudo pacman -S mesa
```

## 2.3 Enable Vulkan

- Install the vulkan loader and driver:
```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

## 2.4 Reboot Your System 
- Reboot your System to apply the changes. 

## 2.5 Validate Installation
- If you want to validate if your graphics, you can do run the following:
```
lsmod | grep pan
```
The output of the command above should indicate that the `panthor` module is loaded. If you still see the `panfrost` module listed, you may want to check if you have done all steps described in this article.

# 3. Revert to Panfrost
- To revert to `Panfork`, run the following commands:

### Tabset {.tabset}
#### UEFI-based System
```
sudo pacman -S mesa-panfork-git
rm /boot/efi/dtb/overlays/rockchip-rk3588-panthor-gpu.dtbo
sudo reboot
```
#### U-Boot-based System
```
sudo pacman -S mesa-panfork-git
sudo nano /boot/extlinux/extlinux.conf
```

Remove the line `fdtoverlays /boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`. 
Then Save and Close.

- Reboot your system to apply your changes:

```
sudo reboot
```

