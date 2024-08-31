---
title: 🐾 How to setup Panthor on Mali GPUs with RK3588
description: 
published: true
date: 2024-08-31T16:00:18.542Z
tags: 
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# Enabling Panthor on Mali GPUs with RK3588 🚀

This guide walks you through the steps to enable Panthor on Mali GPUs present in boards with the RK3588 chipset.

# 🔧 Steps to Enable Panthor 

## On UEFI enabled devices

### 🖥️ 1. Initial Setup on UEFI 

First, create the necessary directories for the DTB files:

```
sudo mkdir -p /boot/dtb/{base,overlays}
```

Next, configure your UEFI settings. Boot into UEFI > Device Manager > Rockchip Platform Configuration > ACPI / Device Tree, and do the following:

- **Set `Config Table Mode` to `Device Tree`**
- **Change `Support DTB override & overlays` to `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

Press F10 to save and boot into your system (you can go back to the first UEFI screen and select `Continue`).


### 🛠️ 3. Setup Device tree

> If you are using a FydeTab Duo, copy the specific DTB file to the `base` folder:
> 
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb /boot/dtb/base/
> sudo cp /boot/dtb/base/rk3588s-fydetab-duo.dtb /boot/dtb/base/rk3588s-tablet-12c-linux.dtb
> ```
{.is-info}

For other RK3588-based boards, replace `rk3588-board.dtb` with your actual device name:

``` 
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb /boot/dtb/base/
```

### 🌐 4. Common Setup for All Boards 

Regardless of the board you are using, copy the DTBO overlay file to enable Panthor:

``` 
sudo cp /boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo /boot/dtb/overlays/
```

### 🔄 5. Replace mesa-panfork-git 

Replace the `mesa-panfork-git` package with the standard `mesa` package:

```  
sudo pacman -S mesa
``` 

### 🔁 6. Reboot Your System 


## ⚙️ On U-Boot Enabled devices 
### 1. Enable the Panthor DTBO

Edit the `extlinux` configuration file to apply the overlay:

```  
sudo nano /boot/extlinux/extlinux.conf
``` 

Add the following line to the `extlinux.conf` file:

```  
fdtoverlays /dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo
``` 

### 🔄 2. Replace mesa-panfork-git 

Replace the `mesa-panfork-git` package with the standard `mesa` package:

```  
sudo pacman -S mesa
``` 

### 🔁 3. Reboot Your System 
