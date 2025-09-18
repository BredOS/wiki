---
title: to be added to orion
description:
published: true
date: 2025-09-17T00:43:12.600Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:43:12.600Z
---

# 簡介

how to switch to the custom bredos fork of the radxa bios

## 2 Download bios

link tbd

## 3. install

## 3.1 Using a USB flash drive

format to fat32
extract contents to the root directory
![flashdrive-listing.png](/orion/flashdrive-listing.png)
reboot go into bios then boot manager `UEFI shell` it should auto start
note for editor ask for pics, i dont have the KVM setup yet

## 3.2 Using a CH341A

## 3.2.1 Prepare

```
sudo pacman -S flashrom
```

get size in bytes

```
du ./cix_flash_all.bin
```

```
6288062 ./cix_flash_all.bin
```

write

```
dd if=/dev/zero bs=1 count=$((8388608 - replaceme)) >> ./cix_flash_all.bin
```

## 3.2.2 hw connection

[sata-firmware-fix](/en/itx-3588j/sata-firmware-fix) # same ways

## 3.2.3 write

sudo flashrom -p ch341a_spi -w ./cix_flash_all.bin

