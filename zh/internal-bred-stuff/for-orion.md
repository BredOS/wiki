---
title: 添加到orion中
description:
published: true
date: 2025-09-17T00:43:12.600Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:43:12.600Z
---

# 简介

如何切换到radxa bios的自定义bredos fork

## 2 下载 bios

链接 tbd

## 3. 安装

## 3.1 使用USB闪存驱动器

格式为 fat32
提取内容到根目录
！[flashdrive-listing.png](/orion/flashdrive-listing.png)
重启后进入bios ，然后启动管理器 `UEFI shell` 后自动启动
编辑器索取图片的笔记， i 尚未安装 KVM

## 3.2 使用CH341A

## 3.2.1 Prepare

```
sudo pacman -S flashrom
```

获取字节大小

```
du ./cix_flash_all.bin
```

```
6288062 ./cix_flash_all.bin
```

写

```
dd if=/dev/n0 bs=1 count=$(8388608-替换)) >> ./cix_flash_all.bin
```

## 3.2.2 小时连接

[sata-firmware-fix](/en/itx-3588j/sata-firmware-fix) # 相同的方式

## 3.2.3 写

sudo flashrom -p ch341a_spi -w ./cix_flash_all.bin

