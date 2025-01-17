---
title: Device Trees
description: 
published: true
date: 2024-11-11T11:50:39.940Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# Device Trees
Device trees is a mechanism for describing hardware in Linux ARM systems, allowing the kernel to discover and configure hardware devices without changing the kernel driver code, Unlike x86 systems, where the ACPI tables  enable automatic hardware discovery and configuration, ARM systems have to change the device tree once the hardware is changed.

## Updating Device Trees in UEFI and Grub systems
Edit the grub configuration file `/etc/default/grub`, find the line that starts with `GRUB_DTB=` and add the path to the device tree file, for example:

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```
Then update the grub configuration:
```bash
sudo update-grub
```

## Updating Device Trees in U-Boot systems with extlinux
Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`, find the line with `fdt`, for example:

```bash
fdt /dtbs/rockchip/xxx.dtb
```
Then reboot.
