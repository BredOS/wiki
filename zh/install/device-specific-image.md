---
title: 安装设备特定图像
description:
published: true
date: 2025-10-22T08:35:52.202Z
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

# 3. 启动设备

- 选择您想要安装 BredOS 的存储设备：

### Tabset {.tabset}

#### SD 卡

<details><summary><b>有SD卡适配器</b></summary>

将 SD 卡插入您的 PC 的 SD 卡读卡器并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)

</details>

<details><summary><b>没有SD卡适配器</b></summary>

将您的 SD 卡插入您的 SBC 并根据您的 PC OS 在部分 [**4.2 与 RKdeveloped tool**](#h-4-2-with-rkdeveloptool)中找到的指南继续。

> 在刷入之前，您必须将目标设备设置为“sd card”。 To do so have a look at [4.2 Changing flash target](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target).
> {.is-info}

</details>

#### 不可移除的 eMMC

<details><summary><b>使用 RKdeveloped 工具</b></summary>

根据您在 [**4.2 与 RKdevelopttool**](#h-4-2-with-rkdeveloptool) 中找到的 PCOS 继续使用指南

</details>

#### 可移动eMMC

<details><summary><b>With eMMC to USB Adapter</b></summary>

由于几乎所有已知的 USB Sticks 都是基于eMC 存储设备，在那里有 USB 到 eMMC 适配器，这些适配器是 USB-Stics ，但是可以移除eMMC 存储设备。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 这些也可以用于闪烁BredOS。 如下面屏幕截图所示，将eMMC连接到您的适配器。

<details><summary><b>USB 到 eMMC 适配器</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

Then continue with [**4.1 with Storage Adapter**](#h-41-with-storage-adapter).

</details>

<details><summary><b>有uSD 适配器</b></summary>
eMMC 基本上是一个 SD 卡，它是硬线到 SBC 的 (大多) SD卡，有适配器可以连接您的 eMC 将它们转换为 SD 卡。

<details><summary><b>uSD Adpater and eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details><summary><b>uSD 适配器连接到阅读器</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

</details>

Then continue with [**4.1 with Storage Adapter**](#h-41-with-storage-adapter).

</details>

<details><summary><b>没有适配器</b></summary>

将您的 eMMC 连接到您的 SBC 并根据您在 [**4.2 与 RKdevelopttool**](#h-4-2-with-rkdeveloptool)中发现的PC操作系统继续使用指南。

</details>

#### NVME

> 由于我们的设备不支持直接从NVMe驱动器启动，我们需要将UEFI安装到另一个介质。 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide. 在 UEFI 启动后，您可以直接从 NVMe 驱动器启动。 在 UEFI 启动后，您可以直接从 nVME 驱动器启动。 To install UEFI to your SPI or SD Card follow this guide.
> {.is-warning}

<details><summary><b>使用 USB 适配器</b></summary>

通过 USB 适配器将驱动器连接到您的电脑并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)。 直接或通过 USB 适配器将驱动器连接到您的电脑。 After flashing connect the drive to the nVME port of your SBC.

</details>

<details><summary><b>没有适配器</b></summary>

将您的 NVMe 驱动器直接连接到您的 PC 并继续 [**4.1 与存储适配器**](#h-41-with-storage-adapter)。 您可能必须强制您的刷入工具写入硬盘。

</details>

# 🚀 4. 刷入

> 我们提供了压缩为.xz文件的图像。 请确保你在刷入之前解压他们！
> {.is-warning} 请确保你在刷入之前解压他们！
> {.is-warning}

## 4.1 与存储适配器

有无数工具刷入sd 卡或 eMMC。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager` 。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

## 4.2 使用 RKdeveloped 工具

为了涵盖您可以为此使用的操作系统，我们决定将安装分成这两个指南：

- [在 Linux 或 macOS下与 RKDevelop 一起刷新](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [Flashing with RKDevelop under Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
