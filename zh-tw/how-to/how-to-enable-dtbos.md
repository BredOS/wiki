---
title: Enable DTB overlays
description:
published: true
date: 2025-09-17T05:43:38.077Z
tags:
editor: markdown
dateCreated: 2024-11-10T18:02:07.427Z
---

# 1. 簡介

Enabling different Device Tree Overlays (DTBOs) allows optional hardware or kernel modifications to be enabled, without recompiling the linux kernel.

> This is also the intended way alter the behavior of the kernel. For example to enable the panthor graphics stack or disable the led on your system.
> {.is-success}

# 2. BredOS-Config

- The bredos-config tool offers a simple way to enable and disable dtbos. Start the tool with

```
sudo bredos-config
```

Then navigate to `Device Tree Manager` -> `Enable / Disable Overlays` and enable dtb overlays to your liking. The tool then installs the base device tree and the selected overlays. Reboot your system to apply the changes.

While bredos-config is able to install dtbs and alter the grub config to load them on boot it _cannot_ alter UEFI settings. This has to be done by the user. The changes the user has to made are shown by bredos-config on first installation of base/overlay dtbs or with `3.4 Configure UEFI`. If your device is `u-boot-based` no further changes are needed.

> If during board power-on you see a BredOS logo, you are using UEFI.
> {.is-warning}

> This is the recommended way to enable/disable dtb overlays. The following steps are not neccessary if you use `bredos-config`.
> {.is-success}

# 3. UEFI-based Systems

If you are running on a UEFI-powered board, you need to configure it.
If you have already done this before you can skip ahead to step 5.

> Images after 12th of September 2024 use `/boot/efi` instead of `/boot`.
> {.is-info}

To determine where your ESP partition is located, run the command, `df | grep "/boot" | awk '{print $NF}'` and replace `<ESP>` in all the following commands with it's output.

## 3.1 Create the necessary directories

- Create the necessary directories for storing the DTB files

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

## 3.2 Copy over the base DTB

> If you are using a FydeTab Duo, copy the specific DTB file to the `base` folder:
>
> `sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/`
> `sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tablet-12c-linux.dtb`
> {.is-info}

- For other RK3588-based boards, replace `rk3588-board.dtb` with your actual device name:

```
sudo cp /boot/dtbs/rockchip/<your-board-name.dtb> <ESP>/dtb/base/
```

## 3.3 Configure GRUB

- Open the GRUB configuration file:

```
sudo nano /etc/default/grub
```

- Comment out the following line by adding a `#` at the beginning:

```
# GRUB_DTB="dtbs/rockchip/<your-board-name.dtb>"
```

- Update GRUB with the new configuration:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 3.4 Configure UEFI

- Reboot into UEFI

> If you need help there is a [guide](/en/how-to/change-default-boot-order-rk3588) to change the boot order. In its first steps it shows you how to boot into UEFI Settings.
> {.is-info}

- Navigate to `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`

- Set `Config Table Mode` to `Device Tree`

- Change `Support DTB override & overlays` to `Enabled`

![](/panthor/enable_tree_dtb_in_uefi.jpg)

- Press F10 to save and reboot back into your system.

## 3.5 Copy the DTBO

- Replace `<my-overlay>` with the dtbo of your choice.

```
sudo cp /boot/dtbs/rockchip/overlay/<my-overlay.dtbo> <ESP>/dtb/overlays/
```

## 3.6 Reboot

- Reboot your system to apply the change.

# 4. U-Boot-based Systems

## 4.1 Edit the extlinux configuration

- The extlinux configuration can be edited by running:

```
sudo nano /boot/extlinux/extlinux.conf
```

- Add the following line to the bottom of the file, replacing the DTBO with the one of your choosing:

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```

> **DO NOT** add more than one `fdtoverlays` line.
> If you wish to enable more than one DTBOs, append them onto the one line, seperated by a whitespace.
> For example:
>
> `fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo`
> {.is-warning}
