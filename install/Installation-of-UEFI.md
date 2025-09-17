---
title: Installation of UEFI (on RK3588)
description: 
published: false
date: 2025-09-17T00:08:03.762Z
tags: 
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. Introduction
Many of our supported devices do offer support for `UEFI`, which is a modern firmware interface that initializes hardware and starts the operating system. With the help of `UEFI` your device is capable of booting .iso files (written to a USB-Stick or burned to a DVD) as well as booting your OS directly from the nVME drive or over the network via PXE.

# 2. Examine your device
Sadly, not all devices we support do support booting `UEFI`. Also, not every device does come with an SPI chip installed. 


- To determine what your device is capable of, check [this table](/en/table-of-supported-devices).

# 3. Installation
- Download the latest release of our UEFI build [here](https://github.com/BredOS/edk2-rk3588/releases).

## 3.1 Installation to SD Card
Download the latest release matching your device, insert a SD Card of (almost) any size into your writer and use your prefered flashing tool. We recommend the use of:

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)
> 
> Insert your SD Card into your SBC and you are good to go!
{.is-success}

## 3.2 Installation to SPI
> If you have skipped 3.1, go back. This step is needed for flashing to the SPI chip!
> You can remove the SD Card afterwards
{.is-info}

> This procedure is untested. If you have done it successfuly please report back on our Discord or Telegram channel.
{.is-warning}


Follow the steps down below to install `UEFI` to your SPI chip.

- Copy the latest release of our `UEFI` to a FAT32 formated USB-Stick and connect it to your SBC. 
- Boot up your board into `UEFI` from your SD Card. If you have trouble to get into UEFI Settings check [this guide](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- Navigate to `Boot Manager` -> `UEFI Shell` to enter the command line interface.
- List all readable partitions with the use of the `map` command. This command lists all partitions with the namingscheme of `fs0:`, `fs1:`, ...
- Navigate to the USB-Stick containing the firmware image by typing the file system name and press `Enter` to change directory to it. If you're unsure which file system to use, run ls fsX: to list its contents.
- Flash `UEFI` to your SPI chip with the command:
```
sf updatefile <FIRMWARE.img> 0x0
```
- Power down your SBC and remove the SD Card.

> Now your device is capable of all the nice UEFI goodies!
{.is-success}
