---
title: Installation with a device specific image
description: 
published: true
date: 2025-10-03T04:59:17.765Z
tags: 
editor: markdown
dateCreated: 2025-09-15T12:36:27.362Z
---

# 1. Introduction
For the installation of BredOS we provide device specific images which are tailored to work out of the box for its specific device. This distinguishes these images from installation via an ISO image. Installation via an ISO image is much more generic, but is supported beyond the devicesupport we offer. 
> If you can't find your device on our download site and your device supports booting via UEFI, feel free to give the ISO installation a try.
{.is-info}


# 2. Download
You can find download links for images in our [website](https://bredos.org/download.html)!

# 3. Installation
Installation varies from device to device and the medium you want to install BredOS to. In this guide we will cover installation to
- [3.1 non-removable eMMC](#h-31-non-removable-emmc)
- [3.2 removable eMMC and SD Card](#h-32-removable-emmc-and-sd-card)
- [3.3 NVMe](#h-33-nvme)

> Before you begin please check which options are available with your device!
{.is-info}


## 3.1 non-removable eMMC
To cover the variety of operating systems you can use for this, we decided to split the installation to non-removable eMMC into these two guides:

 - [Flashing the eMMC with Linux or macOS](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
 - [Flashing the eMMC with Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
 
## 3.2 removable eMMC and SD Card
> If you are familiar with flashing Raspberry OS no further reading is needed. Just grab your SD-Card or eMMC, your device specific BredOS image and flash with your preferred tool.
{.is-info}

In the following we describe how to flash eMMC with an adapter. If you do not own a suitable adapter leave the eMMC connected to your SBC and follow [3.1 non-removable eMMC](#h-31-non-removable-emmc).
### 3.2.1 Get your removable eMMC ready
> Skip to [3.2.2 Flashing eMMC / SD Card](#h-322-flashing-emmc-sd-card) if you are not using eMMC storage.
{.is-info}

#### 3.2.1.1 with uSD adapter
- As a eMMC is basically an SD Card which is (mostly) hardwired to the SBC there are adapters you can connect your eMMC to convert them into an SD Card.

<details>
<summary><b>uSD Adpater and eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
- Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details>
<summary><b>uSD Adapter connected to reader</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)
  
  </details>

#### 3.2.1.2 with USB to eMMC adapter
- As almost all commonly known USB Sticks are based on eMMC storage there are USB to eMMC adapters out there which are USB-Sticks but with removable eMMC storage. These can be used to flash BredOS too.

<details>
<summary><b>USB to eMMC adapter</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)
   </details>

### 3.2.2 Flashing eMMC / SD Card
There are countless tools to flash an sd card or eMMC. We recommend the use of `BalenaEtcher` or `Raspberry Pi Imager`. Both tools offer support for Linux, macOS and Microsoft Windows. 

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> We provide images compressed as .xz files. Make sure you decompress them before flashing!
{.is-warning}


## 3.3 NVMe
### 3.3.1 Preperation
As direct booting from the NVMe drive is not supported by our devices we need to install UEFI to a different medium. After UEFI is booted you then are able to boot from the nVME drive directly. To install UEFI to your SPI or SD Card follow [this guide](/en/install/Installation-of-UEFI).

### 3.3.2 Flashing NVMe
Connect the drive to your PC, either directly or via a USB adapter. Then use one of the recommended tools in [3.2.2 Flashing eMMC / SD Card](#h-322-flashing-emmc-sd-card), making sure to use the correct drive letter or path for your NVMe drive. After flashing connect the drive to the NVMe port of your SBC.

### 3.3.3 Boot Order
The UEFI should be able to pick up the drive by itself. However the order of devices it will try to boot from can slow down the bootprocess or even fail completely (e. g. if you have a PXE Server in your network). To change the bootorder follow this [guide](/en/how-to/change-default-boot-order-rk3588).

> After successful installation proceed with [**First Setup**](/en/install/first-setup)
{.is-success}
