---
title: How to boot from a NVMe drive
description: This guide shows how to setup booting from a NVMe drive
published: true
date: 2025-09-13T12:27:51.814Z
tags: rock-5, rock-5b, rock-5bp, nvme
editor: markdown
dateCreated: 2024-09-21T09:09:29.723Z
---

# 🚀 Booting BredOS from NVMe on Rock 5B/5B Plus

To boot BredOS from an NVMe SSD on the Rock 5B or Rock 5B Plus, you'll need to follow a few steps to prepare your device.

These instructions assume your Rock 5B/5B Plus is already booted into Linux (either from an eMMC or microSD card) and has network connectivity. If you're offline, copy the necessary files to external media like a USB stick to access them.

---

## 🔄 1. Update UEFI Firmware

First, make sure you have the latest UEFI firmware installed. You can easily install the required package from the BredOS repository.

For the **Rock 5B**, use the following command:

```bash
sudo pacman -Sy rock-5b-uefi
```

For the **Rock 5B Plus**, use this:

```bash
sudo pacman -Sy rock-5bplus-uefi
```

## 📦 2. Flash UEFI to SPI

Next, you'll need to flash the UEFI firmware to your device's SPI memory.

For the **Rock 5B Plus**, use the following command:

```bash
sudo dd if=/usr/share/edk2/rock-5bplus/rock-5bplus_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

For the **Rock 5B**, use this:

```bash
sudo dd if=/usr/share/edk2/rock-5b/rock-5b_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

## 📥 3. Write BredOS Image to NVMe

Once the UEFI is flashed, you'll need to download the latest BredOS image from the [Images](https://github.com/BredOS/images/releases) repository. Extract the image file and then use the `dd` command to write the image to your NVMe SSD.

Make sure you replace `/dev/nvme0n1` with the correct path to your NVMe drive.

```bash
sudo dd if=/path/to/bredos_image.img of=/dev/nvme0n1 bs=4M status=progress
```

---

🎉 Once the process is complete, reboot your Rock 5B/5B Plus and it should boot from the NVMe SSD! 

> Do not keep the SDcard or EMMC connected when booting from NVMe as it will make it so your device wont boot!!
{.is-warning}

