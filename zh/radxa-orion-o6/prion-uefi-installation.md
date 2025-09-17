---
title: 更新Orion O6上的 UEFI
description:
published: false
date: 2025-09-17T06:45:47.183Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. 简介

本指南将引导您更新您的Radxa Orion O6 `UEFI`固件到 BredOS。

# 2. 功能

- 前面面板 USB 端口已修复
- CPU 速度被固定为实际运行为 2.6GHz
- ACPI 修复
- 修复蓝牙/wifi卡
- M.2 ssds 不随机变形
- `UEFI`分辨率修复

# 3. 安装

## 3.1 前提条件

- `UEFI`安装.zip文件
- 对于当时的更新 -> FAT32 格式化USB Stick。
- 通过粉丝-> 基于CH341A的粉丝进行更新

这里可以订购一个非常便捷的包，包括烧录机、片段和其他有用的配件：
https://www.aliexpress.com/item/3226327388.html
[spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> 如果链接已过期，请随时在 Discord 或 Telegram 上给我们头部。

## 3.2 当时的更新

您可以通过以下步骤从Radxa UEFI内部安装我们的`UEFI`固件：

- 将您的 USB 棒格式化为 FAT32 并将压缩文件的内容放入驱动器的根目录。
- 您的 USB 棍棒的内容应显示如下：

```
Buildoptions  
BurnImage.efi  
cix_flash_all.bin  
cix_flash_ota.bin  
FlashUpdate.efi  
Shell.efi  
startup.nsh  
VariableInfo.efi
```

- 启动你的棋盘到 `UEFI` 如果您在访问 UEFI 设置时遇到问题，请检查 [本指南] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。
- 浏览至`Boot Manager` -> `UEFI Shell` 以进入命令行接口。
- 更新过程应该自动开始。

> 更新成功后，关闭棋盘并断开电源至少10秒！
> {.is-warning}

## 3.3 通过粉丝更新
