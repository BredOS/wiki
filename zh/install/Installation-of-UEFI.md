---
title: 安装UEFI(RK3588)
description:
published: true
date: 2025-09-23T09:39:06.625Z
tags:
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. 简介

我们支持的许多设备确实为“UEFI”提供支持，这是一个启动硬件并启动操作系统的现代固件接口。 我们支持的许多设备确实为“UEFI”提供支持，这是一个启动硬件并启动操作系统的现代固件接口。 在`UEFI`的帮助下，您的设备能够启动 。 这样文件 (写入 USB-Stick 或烧毁到 DVD) 以及直接从 nVME 驱动器或通过 PXE 在网络上启动您的操作系统。

> UEFI 的多个安装在保存您的 UEFI 设置时可能造成问题。
> {.is-warning}
> {.is-warning}

# 2. 检查您的设备

不幸的是，我们所支持的并非所有设备都支持启动 \\`UEFI'。 而且，并非每个设备都安装了SPI 芯片。 而且，并非每个设备都安装了SPI 芯片。

- To determine what your device is capable of, check [this table](/en/table-of-supported-devices).

# 3. 安装

- 下载我们的 UEFI 版本的 [here](https://github.com/BredOS/edk2-rk3588/releases)。

## 3.1 SD 卡安装

下载与您的设备匹配的最新版本，向您的写作者输入任何大小的 SD 卡并使用您预感刷入工具。 我们建议使用： 我们建议使用：

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> 将SD卡插入SBC，您很好！
> {.is-success}
> {.is-success}

## 3.2 安装SPI设备

> 如果您跳过了3.1，请回来。 需要这个步骤来刷入SPI芯片！
> 您可以在此后移除SD卡。
> {.is-info}

> 这一程序尚未经过测试。 如果您成功完成了这项工作，请在我们的 Discord 或 Telegram 频道上汇报。
> {.is-warning}

按照下面的步骤安装`UEFI`到你的SPI 芯片。

- 将我们的`UEFI`的最新版本复制到FAT32格式的 USB-Stick 并连接到您的 SBC。
- 从你的SD卡上启动你的棋盘到`UEFI`。 如果您在访问 UEFI 设置时遇到问题，请检查 [本指南] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。 如果您在访问 UEFI 设置时遇到问题，请检查 [本指南] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。
- 浏览至`Boot Manager` -> `UEFI Shell` 以进入命令行接口。
- 列出使用`map`命令的所有可读分区。 列出使用`map`命令的所有可读分区。 此命令列出所有分区与 fs0:`, fs1:`...
- 输入文件系统名称并按 `Enter` 键将目录更改为包含固件图像的 USB-Stick 。 如果您不确定要使用哪个文件系统，请运行以下列出其内容： 如果您不确定要使用哪个文件系统，请运行以下列出其内容：

```
ls fs<your drive number here>: 
```

- 用命令刷入 `UEFI` 到 SPI 芯片：

```
sf 更新文件 <FIRMWARE.img> 0x0
```

- 请关闭您的SBC并移除SD卡。

> 现在你的设备能够获得所有好的 UEFI 谷物！
> {.is-success}
> {.is-success}
