---
title: 更新Orion O6上的 UEFI
description:
published: true
date: 2025-10-30T12:49:48.767Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. 简介

- 本指南将引导您更新您的Radxa Orion O6 `UEFI`固件到 BredOS。

![radxa-bios.png](/orion/radxa-bios.png)

# 2. 功能

- 前面面板 USB 端口已修复
- CPU 速度被固定为实际运行为 2.6GHz
- ACPI 修复
- 修复蓝牙/wifi卡
- M.2 ssds 不随机变形
- `UEFI`分辨率修复
- 降低PCIe连接速度的能力。

# 3. 安装

## 3.1 前提条件

- The `UEFI` installation .zip file found [here](/orion/bios.zip).
- 对于一个 "3.2 现场更新" -> FAT32 格式化 USB Stick。
- 对于`3.3 通过 flasher` -> 基于 CH341A的刷新器

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

- 启动你的棋盘到 `UEFI` 启动你的棋盘到 `UEFI` 如果您在访问 UEFI 设置时遇到问题，请检查 [本指南] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。
- 浏览至`Boot Manager` -> `UEFI Shell` 以进入命令行接口。
- 更新过程应该自动开始。

> 更新成功后，关闭棋盘并断开电源至少10秒！
> {.is-warning}
> {.is-warning}
> {.is-warning}
> {.is-warning}

## 3.3 通过粉丝更新

如果你在启动 _Prions_ `UEFI` 时遇到麻烦，或者更喜欢使用 flasher，跟随以下步骤。

> 确保你的火焰被设置为 **1.8 伏特** ！ 使用1.8V适配器。
> {.is-warning}

### 启动你的棋盘到 `UEFI` 如果您在访问 UEFI 设置时遇到问题，请检查 [本指南] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。

- 安装工具 `flashrom` 。

 ```
 sudo pacman -S flashrom
 ```

- 解包 UEFI .zip 文件，并标识UEFI 二进制文件的大小。

```
du ./cix_flash_all.bin
```

- 输出将以字节显示您的大小。

```
6288062 ./cix_flash_all.bin
```

在上面的例子中，文件大小是 `6288062` 。

- 为了匹配chip的规格，我们需要在文件末尾加上“零”，直到它匹配chip的大小。 用上面命令中的文件大小替换<your file size here> 用上面命令中的文件大小替换<your file size here> 用上面命令中的文件大小替换<your file size here> 用上面命令中的文件大小替换<your file size here>

```
dd if=/dev/n0 bs=1 count=$(8388608- <your file size here>)) >> ./cix_flash_all.bin
```

### 3.3.2 连接到SPI

> 确保你的棋盘在移除或插入SPI芯片时断电！
> {.is-warning}
> {.is-warning}
> {.is-warning}
> {.is-warning}

Prion上的 SPI 芯片被套接以便轻松移除。 套接字位于CPU粉丝头和 GPIO 端口。 套接字位于CPU粉丝头和 GPIO 端口。 要轻松定位芯片，请参阅Radxa [在这里找到](https://radxa.com/orion/o6/marked_orion_o6.webp)的文档。

- 套接字具有两层，必须先打开，然后才能移除芯片。

![prion-spi-loaction-cut.png](/orion/prion-spi-loaction-cut.png)

- 从 Prion 中移除SPI 芯片。
- 将 1.8 Volt 适配器连接到您的烧录器。
- 将 ZIF 板连接到 1.8 Volt 适配器。
- Pin 1用芯片上的一个点标记。 Pin 1用芯片上的一个点标记。 当面对你的 USB 端口时，引脚的 1 在左上侧。 请参阅下面的屏幕截图以使方向正确： 请参阅下面的屏幕截图以使方向正确：

![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)

- 将芯片插入ZIF连接器。

### 如果您看到文本"VERIFIED"，固件已被正确刷入。 如果你使用了片段，简单地断开它的连接，你很好。 如果你去除芯片，你知道要做什么。

- 将闪光灯连接到您的电脑并开始刷入：

```
sudo flashrom -p ch341a_spi -w ./cix_flash_all.bin 
```

> 如果您看到文本"VERIFIED"，固件已被正确刷入。 如果你使用了片段，简单地断开它的连接，你很好。 如果你去除芯片，你知道要做什么。
> {.is-success}
