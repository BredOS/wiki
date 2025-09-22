---
title: オリオンに加えられるために
description:
published: true
date: 2025-09-17T00:43:12.600Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:43:12.600Z
---

# はじめに

radxaバイオスのカスタムbredosフォークに切り替える方法

## 2つのプロフィールをダウンロード

リンク tbd

## 3. インストール

## 3.1 USBフラッシュドライブの使用

format to fat32
extract contents to the root directory
![flashdrive-listing.png](/orion/flashdrive-listing.png)
reboot go into bios then boot manager `UEFI shell` it should auto start
note for editor ask for pics, i dont have the KVM setup yet

## 3.2 CH341A の使用

## 3.2.1 Prepare

```
sudo pacman -S flashrom
```

バイト単位でサイズを取得する

```
du ./cix_flash_all.bin
```

```
6288062 ./cix_flash_all.bin
```

書き込み

```
dd if=/dev/zero bs=1 count=$((8388608 - replaceeme)) >> ./cix_flash_all.bin
```

## 3.2.2 hw 接続

[sata-firmware-fix](/en/itx-3588j/sata-firmware-fix) # 同じ方法

## 3.2.3 書き込み

sudo flash -p ch341a_spi -w ./cix_flash_all.bin

