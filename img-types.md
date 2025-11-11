---
title: Image types explained
description: 
published: false
date: 2025-11-11T07:44:16.266Z
tags: 
editor: markdown
dateCreated: 2025-10-25T18:12:07.047Z
---

# 1. Introduction

This page explains the differences between the available image types provided for our platform. Each image type is built using a different Linux kernel base or is tailored in a way that affects hardware support, stability, and update frequency. Understanding these differences will help you choose the image that best fits your development or production needs.

# 2. Device Images
We offer so called "device images". Think of these images like Raspberry Pi's Raspberry OS .img file that one must flash onto an SD card — device images are basically that but not for a Raspberry Pi.  These images are mostly based on a reference kernel made by the SOC manufacturer, ensuring optimal hardware support while relying on a kernel that is poorly maintained. Normally, these kernels function well at release but deteriorate over time as new features are added to the kernel and required by software.  

Of course, we do all we can to address the degradation of the kernel, but there are limits to what can be done. 

> We want to provide mainline support for a handful of devices we currently ship only device images for. 
> [Click here](/en/campaigns/mainline-campaign) for more info.
{.is-info}

## 2.1 Legacy (stable)
These images are based on the reference (also known as BSP) kernel made by the manufacturer of your board and/or SoC. As described above, these images support most of your SBC's features.

## 2.2 Cutting Edge
These ISO images are based on the linux-next branch of the mainline kernel. While hardware support may not be optimal, they do include the latest and most advanced features of the Linux kernel. To find out what features are and are not supported on this kernel refer to the device page for your board found in the navigation bar left from here.

# 3. ISO Images
If you have ever installed Ubuntu or Arch Linux on your PC, you should be familiar with ISO images. These are virtual CD images that can be booted by your UEFI-based system. Burn them onto a disk or USB stick, and your firmware should pick it up.

## 3.1 BSP Image
For some ARM64-based devices, we offer an ISO image bundled with the reference kernel. These images include the SBCs name in the filename. For example, the image for the Radxa Orion O6 is named BredOS-ORION-O6-[Date]-aarch64.iso.

## 3.2 Mainline Image
This image type is bundled with the Linux mainline kernel and is compatible with x86_64 and ARM64-based boards. Like the Cutting Edge Images, not all features of your ARM64-based board are supported. To find out what features are and are not supported on this kernel, refer to the device page for your board found in the navigation bar to the left from here. For x86_64-based boards, all features supported by any other Linux distribution are supported here as well.

# 4. What image should i use?
This decision depends on your board and the environment in which you want to use it. If you plan to use your board as a desktop, we generally recommend using legacy (also known as BSP) based images. If you are using your board as a server, we would suggest opting for cutting-edge (mainline-based) images, as they provide enhanced security and more bug fixes.

If you are unsure if a feature you need is supported with the mainline kernel, have a look at the device specific page for your board. For every board we ship a mainline kernel, there is a table about supported features.