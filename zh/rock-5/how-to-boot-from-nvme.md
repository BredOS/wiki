---
title: 如何从 NVMe 驱动器启动
description: 本指南显示如何从NVMe驱动器启动程序
published: true
date: 2025-09-17T10：09：37.865Z
tags: 五岩石，五岩，五岩，nvme
editor: markdown
dateCreated: 2024-09-21T09：09：29.723Z
---

# 1. 简介

从NVMe SSD到5B或5B加路启动BredOS， 您需要遵循几个步骤来准备您的设备。

这些说明假设您的 Rock 5B/5B Plus 已经启动到 Linux (或者是来自eMMC 或 microSD 卡)，并具有网络连接。 如果您离线，复制必要的文件到外部媒体，如USB棍棒来访问。 如果您离线，复制必要的文件到外部媒体，如USB棍棒来访问。 如果您离线，复制必要的文件到外部媒体，如USB棍棒来访问。

# 2. 安装

## 2.1 更新 UEFI 固件

首先，请确保您已安装最新的 UEFI 固件。 您可以轻松地从 BredOS 仓库安装所需的软件包。 您可以轻松地从 BredOS 仓库安装所需的软件包。

- 对于**Rock 5B**，请使用以下命令：

```bash
sudo pacman -Sy rock-5b-uefi
```

- 对于**Rock 5B Plus**，请使用：

```bash
sudo pacman -Sy rock-5bplus-uefi
```

## 2.2 紧急UEFI 到 SPI

接下来，你需要刷入 UEFI 固件到你设备的 SPI 内存。

- 对于**Rock 5B Plus**，请使用以下命令：

```bash
sudo dd if=/usr/share/edk2/rock-5bplus/rock-5bplus_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

- 对于**Rock 5B**，请使用：

```bash
sudo dd if=/usr/share/edk2/rock-5b/rock-5b_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

## 2.3 将 BredOS 图像写入到 NVMe

一旦UEFI被刷新，您需要从 [Images](https://github.com/BredOS/images/releases) 仓库下载最新的 BredOS 图像。 解压缩图像文件，然后使用 `dd` 命令将图像写入您的 NVMe SSD 解压缩图像文件，然后使用 `dd` 命令将图像写入您的 NVMe SSD 解压缩图像文件，然后使用 `dd` 命令将图像写入您的 NVMe SSD

- 请确保您用 NVMe 驱动器的正确路径替换 `/dev/nvme0n1` 。

```bash
sudo dd if=/path/to/bredos_image.img of=/dev/nvme0n1 bs=4M status=progress
```

> 从NVMe启动时不要保持SD卡或EMMC连接，因为它会使您的设备启动失败！
> {.is-warning}
> {.is-warning}

> 一旦进程完成，请重启你的 Rock 5B/5B Plus 并从NVMe SSD 启动！
> {.is-success}
