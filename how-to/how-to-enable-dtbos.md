---
title: 📟 How to enable DTBOs
description: 
published: true
date: 2025-05-15T12:59:22.120Z
tags: 
editor: markdown
dateCreated: 2024-11-10T18:02:07.427Z
---

# How to enable Device Tree Overlays
**Introduction**
Enabling different Device Tree Overlays (DTBOs) allows optional hardware or kernel modifications to be enabled, without recompiling the linux kernel.
This is also the intended way to enable the panthor graphics stack.

---

# 💻 For UEFI-powered Systems
If you are running on a UEFI-powered board, you need to configure it.
If you have already done this before you can skip ahead to step 5.

> Images after 12th of September 2024 use `/boot/efi` instead of `/boot`.
{.is-info}

To determine where your ESP partition is located, run the command,
`df | grep "/boot" | awk '{print $NF}'` and **replace **`<ESP>`** IN ALL OF THE FOLLOWING commands** with it's output.

### 📁 1: Create the necessary directories for storing the DTB files

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

### 🗄️ 2: Copy over the base DTB

> If you are using a FydeTab Duo, copy the specific DTB file to the `base` folder:
> 
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tablet-12c-linux.dtb
> ```
{.is-info}

For other RK3588-based boards, replace `rk3588-board.dtb` with your actual device name:

``` 
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

### 🫘 3: Configure GRUB
Open the GRUB configuration file:
```
sudo nano /etc/default/grub
```

Comment out the following line by adding a `#` at the beginning:
```
# GRUB_DTB="dtbs/rockchip/device-tree.dtb"
```
*(Your DTB will be different there)*
  
Update GRUB with the new configuration:
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🎛️ 4: Configure UEFI
Reboot into UEFI *(You can do this from GRUB)* > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`, and do the following:

- **Set `Config Table Mode` to `Device Tree`**
- **Change `Support DTB override & overlays` to `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

Press F10 to save and reboot back into your system (you can go back to the first UEFI screen and select `Continue`).

### 🔄 5: Copy the DTBO
Replace `my-overlay` with the dtbo of your choice. 
``` 
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

### ⏼ 6: Reboot
Reboot your system to apply the change.

# ⚙️ On U-Boot Powered Devices
### 1. Edit the extlinux configuration

The extlinux configuration can be edited by running:

```  
sudo nano /boot/extlinux/extlinux.conf
``` 

Add the following line to the bottom of the file, replacing the DTBO with the one of your choosing:

```  
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
``` 

### IMPORTANT NOTES
**DO NOT** add `/boot` or the `<ESP>` stuff in these lines.

**DO NOT** add more than one `fdtoverlays` line.
If you wish to enable more than one DTBOs, append them onto the one line, seperated by space.
Example:

```
fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
```