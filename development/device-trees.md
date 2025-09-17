---
title: Device Trees
description: 
published: true
date: 2025-09-17T09:59:24.978Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# 1. Introduction
Device trees is a mechanism for describing hardware commonly used in ARM and RISC-V systems, allowing the kernel to discover and configure hardware devices without changing the kernel driver code.
Unlike x86 systems, where the ACPI tables enable automatic hardware discovery and configuration, most ARM systems need to have their device tree modified to declare hardware changes.

# 2. Switching Device Trees
## 2.1 Switching Device Trees in UEFI and Grub systems
Open the grub configuration file `/etc/default/grub`.
- Find the line that starts with `GRUB_DTB=` and add the path to the device tree file, for example:

```bash
GRUB_DTB= dtbs/rockchip/<your device tree here>.dtb
```


- Then update the grub configuration:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
> There can only be one DTB specified.
{.is-info}


## 2.2 Updating Device Trees in U-Boot systems with extlinux
- Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`. Find the line with `fdt`, for example:

```bash
fdt /dtbs/rockchip/<your device tree here>.dtb
```
Then edit it to match your device tree path. Save and reboot your system.

> There can only be one DTB specified.
{.is-info}
