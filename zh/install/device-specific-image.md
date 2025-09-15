---
title: 安装设备特定图像
description:
published: false
date: 2025-09-15T13：16：06.236Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36.362Z
---

# 1. 简介

为了安装 BredOS ，我们提供了特定的设备图像，用于在其特定设备的箱子中解锁。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。

> 如果您在我们的下载网站上找不到您的设备，并且您的设备支持通过 UEFI 启动， 请随时尝试安装ISO 安装。
> {.is-info}

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接

# 3. 安装

安装方式因设备而异，您想要安装 BredOS 的介质。 在本指南中，我们将涵盖安装到

- `3.1 不可移动eMMC`
- `3.2 可移动eMMC 和 SD Card`
- `3.3 nVME`

> 在您开始之前，请检查您的设备上有哪些选项可用！
> {.is-info}

## 3.1 不可移动eMMC

为了覆盖您可以使用的操作系统的多样性，我们决定将安装分成不可移除的 eMMC 到这两个指南：

- 使用 Linux 或 macOS 刷入 eMMC
- 使用 Microsoft Windows 刷入 eMMC

## 3.2 可移动的 eMMC 和 SD 卡

> 如果你熟悉刷新树莓操作系统，不需要进一步阅读。 只需抓取您的 SD 卡或 eMMC，您的设备特定的 BredOS 图像并用您的首选工具闪烁。
> {.is-info}

### 3.2.1 准备好您可移除的 eMMC

> 如果您没有使用 eMC存储设备，请跳至 `3.2.2 刷入eMMC / SD Card` 。
> {.is-info}

#### 3.2.1.1 使用 uSD 适配器

因为eMMC基本上是一个 SD 卡，它(大多是) 硬线到SBC ，有适配器可以连接您的 eMMC 将它们转换成SD卡。
！[usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)
坚定按下 eMMC 的连接器到 uSD 适配器并将它们连接到您的 SD 卡阅读器。
![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

#### 3.2.1.2 使用 USB 为 eMMC 适配器

由于几乎所有已知的 USB Sticks 都是基于eMC 存储设备，在那里有 USB 到 eMMC 适配器，这些适配器是 USB-Stics ，但是可以移除eMMC 存储设备。 这些也可以用于闪烁BredOS。
![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

### 3.2.2 刷入 eMMC / SD 卡

有无数工具刷入sd 卡或 eMMC。 在本指南中，我们将涵盖`BalenaEtcher`和`Raspberry Pi Imager`。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 从下面选择一个指南以继续。

- 正在与BalenaEtcher
- 用树莓派成像器刷入

## 3.3 nVME

### 3.3.1 前提条件

由于我们的设备不支持直接从 nVME 驱动器启动，我们需要安装 UEFI 到另一个介质。 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 若要按照本指南安装UEFI到您的SPI或SD卡，请遵循本指南。

### 3.3.2 Flashing nVME

直接或通过 USB 适配器将驱动器连接到您的电脑。 然后跟随“3.2”中的一个指南。 刷入 eMMC / SD 卡\`，确保你的 NVMe 驱动器使用正确的驱动器字母或路径。 刷入后将驱动器连接到 SBC 的 nVME 端口。

### 3.3.3 启动顺序

UEFI应该能够自己拿起驱动器。 然而，它试图从设备上启动的顺序可能会减慢引导过程或甚至完全失败(e.g.)。 如果您的网络中有一个 PXE 服务器)。 要更改启动器，请按照此 [guide](/en/how-to/change-default-boot-order-rk3588)。

> After successful installation proceed with [**First Setup**](/en/install/first-setup)
> {.is-success}
