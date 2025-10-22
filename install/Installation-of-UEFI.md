---
title: Installation of UEFI (on RK3588)
description: 
published: true
date: 2025-10-22T08:30:35.101Z
tags: 
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. Introduction
Many of our supported devices do offer support for `UEFI`, which is a modern firmware interface that initializes hardware and starts the operating system. With the help of `UEFI` your device is capable of booting .iso files (written to a USB-Stick or burned to a DVD) as well as booting your OS directly from the NVMe drive or over the network via PXE.

> Multiple installations of UEFI can cause problems when saving your UEFI settings.
{.is-warning}


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

## 3.2 Installation to SPI from within UEFI
> If you have skipped 3.1, go back. This step is needed for flashing to the SPI chip!
> You can remove the SD Card afterwards.
{.is-info}

Follow the steps down below to install `UEFI` to your SPI chip.

- Copy the latest release of our `UEFI` to a FAT32 formated USB-Stick and connect it to your SBC. 
- Boot up your board into `UEFI` from your SD Card. If you have trouble accessing the UEFI Settings, check [this guide](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- Navigate to `Boot Manager` -> `UEFI Shell` to enter the command line interface.
- List all readable partitions with the use of the `map` command. This command lists all partitions with the namingscheme of `fs0:`, `fs1:`, ...
- Navigate to the USB-Stick containing the firmware image by typing the file system name and press `Enter` to change directory to it. If you're unsure which file system to use, run the following to list its contents:
```
ls fs<your drive number here>: 
```

- Flash `UEFI` to your SPI chip with the command:
```
sf updatefile <FIRMWARE.img> 0x0
```
- Power down your SBC and remove the SD Card.

## 3.3 Installation to SPI from within BredOS
- If your board is booted into BredOS, it is possible to install UEFI on your SPI by running the following command:
```
sudo dd if=/path/to/downloaded/uefi/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/mtdblock0
```
We recommend following section [3. Flashing the UEFI Firmware](/en/how-to/update-uefi-rk3588#h-3-flashing-the-uefi-firmware) to learn more
- Power down your SBC and remove the SD Card.



> Now your device is capable of all the nice UEFI goodies!
{.is-success}
