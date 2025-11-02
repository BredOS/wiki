---
title: 已解释的图像类型
description:
published: false
date: 2025-11-02T13:00:17.438Z
tags:
editor: markdown
dateCreated: 2025-10-25T18：12：07.047Z
---

# 2. 介绍信息

This page explains the differences between the available image types provided for our platform. Each image type is built using a different Linux kernel base or is tailored in a way that affects hardware support, stability, and update frequency. Understanding these differences will help you choose the image that best fits your development or production needs.

# 2. Device Images

We offer so called "device images". These images are mostly based on a reference kernel made by the SOC manufacturer, ensuring optimal hardware support while relying on a kernel that is poorly maintained. Normally, these kernels function well at release but deteriorate over time as new features are added to the kernel and required by software.

Of course, we do all we can to address the degradation of the kernel, but there are limits to what can be done. Think of these images like Raspberry Pi's Raspberry OS .img file that one must flash onto an SD card — device images are basically that but not for a Raspberry Pi.

> We want to provide mainline support for a handful of devices we currently ship only device images for.
> [Click here](/en/campaigns/mainline-campaign) for more info.
> {.is-info}

# 3. ISO Images

If you have ever installed Ubuntu or Arch Linux on your PC, you should be familiar with ISO images. These are virtual CD images that can be booted by your UEFI-based system. Burn them onto a disk or USB stick, and your firmware should pick it up.

## 3.1 Legacy (stable)

These ISO images are based on the reference (also known as BSP) kernel made by the manufacturer of your board and/or SOC. Like device images, they offer the best hardware support initially but deteriorate quickly.

> Those images are **not** available for the x86_64 architecture, as mainline kernel support is fully fleshed out here.
> {.is-success}

## 3.2 Cutting Edge

These ISO images are based on the linux-next branch of the mainline kernel. While hardware support may not be optimal, they do include the latest and most advanced features of the Linux kernel.

# 4. What image may i use?

This decision depends on your board and the environment in which you want to use it. If you plan to use your board as a desktop, we generally recommend using legacy (also known as BSP) based images. If you are using your board as a server, we would suggest opting for cutting-edge (mainline-based) images, as they provide enhanced security and more bug fixes.