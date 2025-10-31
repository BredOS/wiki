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

为了安装 BredOS ，我们提供了特定的设备图像，用于在其特定设备的箱子中解锁。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。 这将这些图像与通过ISO图像进行的安装区分开来。 通过 ISO 镜像安装更通用，但我们提供的设备支持之外的设备。

> 如果你熟悉刷新树莓操作系统，不需要进一步阅读。 只需抓取您的 SD 卡或 eMMC，您的设备特定的 BredOS 图像并用您的首选工具闪烁。
> {.is-info} Just grab your SD-Card or eMMC, your device specific image and flash with your preferred Tool.
> {.is-info}

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接

# 3. 安装

- 安装方式因设备而异，您想要安装 BredOS 的介质。 在本指南中，我们将涵盖安装到 在本指南中，我们将涵盖安装到 在本指南中，我们将涵盖安装到 在本指南中，我们将涵盖安装到

### Tabset {.tabset}

#### SD 卡

<details>`3.2 可移动eMMC 和 SD Card`

将 SD 卡插入您的 PC 的 SD 卡读卡器并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)

</details>

<details>有无数工具刷入sd 卡或 eMMC。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。

将您的 SD 卡插入您的 SBC 并根据您的 PC OS 在部分 [**4.2 与 RKdeveloped tool**](#h-4-2-with-rkdeveloptool)中找到的指南继续。

> 在刷入之前，您必须将目标设备设置为“sd card”。 在刷入之前，您必须将目标设备设置为“sd card”。 To do so have a look at [4.2 Changing flash target](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target).
> {.is-info}

</details>

#### 不可移除的 eMMC

<details><summary><b>使用 RKdeveloped 工具</b></summary>

根据您在 [**4.2 与 RKdevelopttool**](#h-4-2-with-rkdeveloptool) 中找到的 PCOS 继续使用指南

</details>

#### 可移动eMMC

<details>由于几乎所有已知的 USB Sticks 都是基于eMC 存储设备，在那里有 USB 到 eMMC 适配器，这些适配器是 USB-Stics ，但是可以移除eMMC 存储设备。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。

由于几乎所有已知的 USB Sticks 都是基于eMC 存储设备，在那里有 USB 到 eMMC 适配器，这些适配器是 USB-Stics ，但是可以移除eMMC 存储设备。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 如下面屏幕截图所示，将eMMC连接到您的适配器。

<details><summary><b>USB 到 eMMC 适配器</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

Then continue with [**4.1 with Storage Adapter**](#h-41-with-storage-adapter).

</details>

<details>因为eMMC基本上是一个 SD 卡，它(大多是) 硬线到SBC ，有适配器可以连接您的 eMMC 将它们转换成SD卡。
  ！[usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)
  坚定按下 eMMC 的连接器到 uSD 适配器并将它们连接到您的 SD 卡阅读器。
![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

<details><summary><b>uSD Adpater and eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details><summary><b>uSD 适配器连接到阅读器</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

</details>

Then continue with [**4.1 with Storage Adapter**](#h-41-with-storage-adapter).

</details>

<details>下面我们描述如何用适配器刷入eMMC。 下面我们描述如何用适配器刷入eMMC。 下面我们描述如何用适配器刷入eMMC。 下面我们描述如何用适配器刷入eMMC。 If you do not own a suitable adapter leave the eMMC connected to your SBC and follow [3.1 non-removable eMMC](#h-31-non-removable-emmc).

将您的 eMMC 连接到您的 SBC 并根据您在 [**4.2 与 RKdevelopttool**](#h-4-2-with-rkdeveloptool)中发现的PC操作系统继续使用指南。

</details>

#### NVME

> 由于我们的设备不支持直接从NVMe驱动器启动，我们需要将UEFI安装到另一个介质。 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide. 在 UEFI 启动后，您可以直接从 NVMe 驱动器启动。 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide. 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide.
> {.is-info}

<details>3.2.1.1 使用 uSD 适配器

通过 USB 适配器将驱动器连接到您的电脑并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)。 通过 USB 适配器将驱动器连接到您的电脑并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)。 直接或通过 USB 适配器将驱动器连接到您的电脑。 After flashing connect the drive to the nVME port of your SBC.

</details>

<details>3.1 不可移动eMMC

将您的 NVMe 驱动器直接连接到您的 PC 并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)。 您可能必须强制您的刷入工具写入硬盘。 您可能必须强制您的刷入工具写入硬盘。

</details>

# 🚀 4. 刷入

> 我们提供了压缩为.xz文件的图像。 请确保你在刷入之前解压他们！
> {.is-warning} 请确保你在刷入之前解压他们！
> {.is-warning}

## 4.1 与存储适配器

有无数工具刷入sd 卡或 eMMC。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

## 4.2 使用 RKdeveloped 工具

为了覆盖您可以使用的操作系统的多样性，我们决定将安装分成不可移除的 eMMC 到这两个指南：

- [在 Linux 或 macOS下与 RKDevelop 一起刷新](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [Flashing with RKDevelop under Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
