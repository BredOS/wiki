---
title: Updating UEFI on Orion O6
description: 
published: false
date: 2025-09-17T07:15:55.572Z
tags: 
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. Introduction
This guide will lead you through the process of updating your Radxa Orion O6 `UEFI` firmware to BredOS. 

# 2. Features
- Front Panel USB Port fixed
- CPU speed is fixed to actually running with 2.6GHz
- ACPI fixes
- Fix for bluetooth/wifi cards
- M.2 ssds doesnt dissapear randomly
- `UEFI` resolution fix

# 3. Installation
## 3.1 Prerequisites

 - The `UEFI` installtion .zip file
 - For an `3.2 in-place update` -> FAT32 formated USB Stick
 - For `3.3 Update through flasher` -> A CH341A-based flasher
 
 A very handy pack including the flasher, clip, and other useful accessories can be ordered here:
 https://www.aliexpress.com/item/32263275388.html
 ![spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)
 >If the link has expired, feel free to give us a heads-up on Discord or Telegram.
 
## 3.2 In-place update
You can install our `UEFI` firmware from within the Radxa UEFI by following these steps:

- Format your USB stick to FAT32 and place the contents of the zip file in the root directory of the drive.
- The content of your USB stick should appear as follows:
```
BuildOptions  
BurnImage.efi  
cix_flash_all.bin  
cix_flash_ota.bin  
FlashUpdate.efi  
Shell.efi  
startup.nsh  
VariableInfo.efi
```
- Boot up your board into `UEFI`. If you have trouble accessing the UEFI Settings, check [this guide](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- Navigate to `Boot Manager` -> `UEFI Shell` to enter the command line interface.
- The update process should start automatically.

> After a successful update, shut down the board and disconnect it from the power source for at least 10 seconds!
{.is-warning}


## 3.3 Update through flasher
If you have trouble booting the *Prions* `UEFI` or prefer using a flasher follow the steps below.

> Ensure that your flasher is set to 1.8 volts!
{.is-warning}

### 3.3.1 Prepare
 - Install the tool `flashrom`
 ```
sudo pacman -S flashrom
```
- Unpack the UEFI .zip file and identify the size of the UEFI binary file
```
du ./cix_flash_all.bin
```
- The output will show you its size in bytes
```
6288062 ./cix_flash_all.bin
```
In the example above the file size is `6288062`.

> Note down the file size. Do not copy-paste it from above as size may vary due to updates!
{.is-info}

### 3.3.2 Connect to SPI

> Ensure that your board is disconnected from power while removing or inserting the SPI chip!
{.is-warning}

The SPI Chip on the Prion is socketed for easy removing. The socket is located in between the CPU Fan Header and the GPIO port. 
