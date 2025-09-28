---
title: 安装设备特定图像
description:
published: true
date: 2025-09-28T08:24:20.184Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36.362Z
---

# 1. 简介

为了安装 BredOS ，我们提供了特定的设备图像，用于在其特定设备的箱子中解锁。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。

> 如果你熟悉刷新树莓操作系统，不需要进一步阅读。 只需抓取您的 SD 卡或 eMMC，您的设备特定的 BredOS 图像并用您的首选工具闪烁。
> {.is-info} Just grab your SD-Card or eMMC, your device specific image and flash with your preferred Tool.
> {.is-info}

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接

# 3. 安装

安装方式因设备而异，您想要安装 BredOS 的介质。 在本指南中，我们将涵盖安装到 在本指南中，我们将涵盖安装到 在本指南中，我们将涵盖安装到

- `3.1 不可移动eMMC`
- `3.2 可移动eMMC 和 SD Card`
- [3.3 NVMe](#h-33-nvme)

> 在您开始之前，请检查您的设备上有哪些选项可用！
> {.is-info}
> {.is-info}
> {.is-info}

## 3.1 不可移动eMMC

为了覆盖您可以使用的操作系统的多样性，我们决定将安装分成不可移除的 eMMC 到这两个指南：

- 使用 Linux 或 macOS 刷入 eMMC
- 使用 Microsoft Windows 刷入 eMMC

## 3.2 可移动的 eMMC 和 SD 卡

> 如果你熟悉刷新树莓操作系统，不需要进一步阅读。 只需抓取您的 SD 卡或 eMMC，您的设备特定的 BredOS 图像并用您的首选工具闪烁。
> {.is-info} Just grab your SD-Card or eMMC, your device specific image and flash with your preferred Tool.
> {.is-info}

下面我们描述如何用适配器刷入eMMC。 下面我们描述如何用适配器刷入eMMC。 下面我们描述如何用适配器刷入eMMC。 If you do not own a suitable adapter leave the eMMC connected to your SBC and follow [3.1 non-removable eMMC](#h-31-non-removable-emmc).

### 3.2.1 准备好您可移除的 eMMC

> 如果您没有使用 eMC存储设备，请跳至 [3.2.2 刷入 eMMC / SD 卡](#h-322-flashing-emmc-sd-card)。
> {.is-info}
> {.is-info}
> {.is-info}

#### 3.2.1.1 使用 uSD 适配器

- 因为eMMC基本上是一个 SD 卡，它(大多是) 硬线到SBC ，有适配器可以连接您的 eMMC 将它们转换成SD卡。
  ！[usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)
  坚定按下 eMMC 的连接器到 uSD 适配器并将它们连接到您的 SD 卡阅读器。
  ![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

- 如果您没有使用 eMC存储设备，请跳至 `3.2.2 刷入eMMC / SD Card` 。
  {.is-info}

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

#### 3.2.1.2 使用 USB 为 eMMC 适配器

- 由于几乎所有已知的 USB Sticks 都是基于eMC 存储设备，在那里有 USB 到 eMMC 适配器，这些适配器是 USB-Stics ，但是可以移除eMMC 存储设备。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

### 3.2.2 刷入 eMMC / SD 卡

有无数工具刷入sd 卡或 eMMC。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> 我们提供了压缩为.xz文件的图像。 请确保你在刷入之前解压他们！
> {.is-warning} 请确保你在刷入之前解压他们！
> {.is-warning}

## 3.3 NVMe

### 3.3.1 前提条件

As direct booting from the NVMe drive is not supported by our devices we need to install UEFI to a different medium. 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide.

### 3.3.2 Flashing NVMe

直接或通过 USB 适配器将驱动器连接到您的电脑。 Then follow the steps in `3.2 Removable eMMC and SD Card`, making sure to use the correct drive letter or path for your NVMe drive. After flashing connect the drive to the NVMe port of your SBC.

### 3.3.3 启动顺序

UEFI应该能够自己拿起驱动器。 然而，它试图从设备上启动的顺序可能会减慢引导过程或甚至完全失败(e.g.)。 如果您的网络中有一个 PXE 服务器)。 要更改启动器，请按照此 [guide](/en/how-to/change-default-boot-order-rk3588)。

> After successful installation proceed with [**First Setup**](/en/install/first-setup)
> {.is-success}
