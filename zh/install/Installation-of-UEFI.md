---
title: 安装UEFI(RK3588)
description:
published: true
date: 2025-10-23T06:14:27.097Z
tags:
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. 简介

我们支持的许多设备确实为"UEFI"提供支持，这是一个启动硬件并启动操作系统的现代固件接口。 在`UEFI`的帮助下，您的设备能够启动 .iso 文件（写入 USB 存储设备或烧录到 DVD）以及直接从 NVMe 驱动器或通过 PXE 在网络上启动您的操作系统。

> UEFI 的多个安装在保存您的 UEFI 设置时可能造成问题。
> {.is-warning}

# 2. 检查您的设备

不幸的是，我们所支持的并非所有设备都支持启动 `UEFI`。 而且，并非每个设备都安装了 SPI 芯片。

- 要确定您的设备支持什么功能，请查看[此表格](/en/table-of-supported-devices)。

# 3. 安装

- 从[这里](https://github.com/BredOS/edk2-rk3588/releases)下载我们的 UEFI 版本。

## 3.1 SD 卡安装

下载与您的设备匹配的最新版本，准备任何大小的 SD 卡并使用您喜欢的刷入工具。 我们建议使用：

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> 将 SD 卡插入 SBC，您就完成了！
> {.is-success}

## 3.2 安装到 SPI 芯片

> 如果您跳过了 3.1，请回去完成。 需要这个步骤来刷入 SPI 芯片！
> 您可以在此后移除 SD 卡。
> {.is-info}

按照下面的步骤安装`UEFI`到您的 SPI 芯片。

- 将我们的`UEFI`的最新版本复制到 FAT32 格式的 USB 存储设备并连接到您的 SBC。
- 从您的 SD 卡上启动您的板子到`UEFI`。 如果您在访问 UEFI 设置时遇到问题，请查看[本指南](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu)。
- 浏览至`Boot Manager` -> `UEFI Shell` 以进入命令行接口。
- 使用`map`命令列出所有可读分区。 此命令列出所有分区，如 `fs0:`、`fs1:` 等。
- 输入文件系统名称并按 `Enter` 键将目录更改为包含固件镜像的 USB 存储设备。 如果您不确定要使用哪个文件系统，请运行以下命令列出其内容：

```
ls fs<your drive number here>: 
```

- 用以下命令将 `UEFI` 刷入 SPI 芯片：

```
sf update <FIRMWARE.img> 0x0
```

- 请关闭您的 SBC 并移除 SD 卡。

## 3.3 从 BredOS 内部安装到 SPI

- 如果您的板子已经启动到 BredOS，可以通过运行以下命令在您的 SPI 上安装 UEFI：

```
sudo dd if=/path/to/downloaded/uefi/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/mtd0
```

> 我们建议阅读下一章节 [3. Flashing the UEFI Firmware](/en/how-to/update-uefi-rk3588#h-3-flashing-the-uefi-firmware) 以了解更多信息。
> {.is-info}

- 请关闭您的 SBC 并移除 SD 卡。

> 现在您的设备能够享受所有 UEFI 的好处了！
> 祝您使用愉快！
> {.is-success}
