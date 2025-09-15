---
title: Installation with a device specific image
description:
published: false
date: 2025-09-15T12:47:06.870Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36:27.362Z
---

# 1. Introduction

For the installation of BredOS we provide device specific images which are tailored to work out of the box for its specific device. This distinguishes these images from installation via an ISO image. Installation via an ISO image is much more generic, but is supported beyond the devicesupport we offer.

> If you can't find your device on our download site and your device supports booting via UEFI, feel free to give the ISO installation a try.
> {.is-info}

# 2. Download

You can find download links for images in our [website](https://bredos.org/download.html)!

# 3. Installation

Installation varies from device to device and the medium you want to install BredOS to. In this guide we will cover installation to

- `non-removable eMMC`
- `removable eMMC and SD Card`
- `nVME`

> Before you begin please check which options are available with your device!
> {.is-info}

## 3.1 non-removable eMMC

To cover the variety of operating systems you can use for this, we decided to split the installation to non-removable eMMC into these two guides:

- Flashing the eMMC with Linux or macOS
- Flashing the eMMC with Microsoft Windows

## 3.2 removable eMMC and SD Card

> If you are familiar with flashing Raspberry OS no further reading is needed. Just grab your SD-Card or eMMC, your device specific image and flash with your preferred Tool.
> {.is-info}

### 3.2.1 Get your removable eMMC ready

## 3.3 nVME

### 3.3.1 Prerequisites

As direct booting from the nVME drive is not supported by our devices we need to install UEFI to a different medium. After UEFI is booted you then are able to boot from the nVME drive directly. To install UEFI to your SPI or SD Card follow this guide.

### 3.3.2 Flashing nVME

Connect the drive to your PC, either directly or via a USB adapter. Then follow the steps in `3.2 Removable eMMC and SD Card`, making sure to use the correct drive letter or path for your NVMe drive. After flashing connect the drive to the nVME port of your SBC.

### 3.3.3 Boot Order

The UEFI should be able to pick up the drive by itself. However the order of devices it will try to boot from can slow down the bootprocess or even fail completely (e. g. if you have a PXE Server in your network). To change the bootorder follow this [guide](/en/how-to/change-default-boot-order-rk3588).

> After successful installation proceed with [**First Setup**](/en/install/first-setup)
> {.is-success}
