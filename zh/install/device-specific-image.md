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

为了安装 BredOS，我们提供了特定的设备镜像，用于在其特定设备上开箱即用。 这将这些镜像与通过 ISO 镜像进行的安装区分开来。 通过 ISO 镜像安装更通用，适用于我们提供设备支持之外的设备。

> 如果您熟悉刷写树莓派操作系统，不需要进一步阅读。 只需获取您的 SD 卡或 eMMC，您的设备特定的 BredOS 镜像并使用您首选的工具刷写。
> {.is-info}

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接

# 3. 启动设备

- 选择您想要安装 BredOS 的存储设备：

### Tabset {.tabset}

#### SD 卡

<details><summary><b>有SD卡适配器</b></summary>

将 SD 卡插入您的 PC 的 SD 卡读卡器并继续 [**4.1 使用存储适配器**](#h-41-with-storage-adapter)

</details>

<details><summary><b>没有SD卡适配器</b></summary>

将您的 SD 卡插入您的 SBC 并根据您的 PC 操作系统在 [**4.2 使用 RKDevelopTool**](#h-4-2-with-rkdeveloptool) 中找到的指南继续。

> 在刷写之前，您必须将目标设备设置为"sd card"。 要这样做，请查看 [4.2 更改刷写目标](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target)。
> {.is-info}

</details>

#### 不可移除的 eMMC

<details><summary><b>使用 RKDevelopTool</b></summary>

根据您的 PC 操作系统，在 [**4.2 使用 RKDevelopTool**](#h-4-2-with-rkdeveloptool) 中找到指南继续

</details>

#### 可移动eMMC

<details><summary><b>使用 eMMC 到 USB 适配器</b></summary>

由于几乎所有已知的 USB 存储设备都是基于 eMMC 存储设备，因此有 USB 到 eMMC 适配器，这些适配器类似于 USB 存储设备，但可以移除 eMMC 存储模块。 这些也可以用于刷写 BredOS。 如下面屏幕截图所示，将 eMMC 连接到您的适配器。

<details><summary><b>USB 到 eMMC 适配器</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

然后继续 [**4.1 使用存储适配器**](#h-41-with-storage-adapter)。

</details>

<details><summary><b>使用 uSD 适配器</b></summary>

eMMC 基本上是一个硬连接到 SBC 的 SD 卡。（大多数）SD 卡有适配器可以连接您的 eMMC 将它们转换为 SD 卡。

<details><summary><b>uSD 适配器和 eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>

牢固地将 eMMC 的连接器压到 uSD 适配器上，并将它们连接到您的 SD 卡读卡器。

<details><summary><b>uSD 适配器连接到读卡器</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

</details>

然后继续 [**4.1 使用存储适配器**](#h-41-with-storage-adapter)。

</details>

<details><summary><b>没有适配器</b></summary>

将您的 eMMC 连接到您的 SBC 并根据您的 PC 操作系统在 [**4.2 使用 RKDevelopTool**](#h-4-2-with-rkdeveloptool) 中发现的指南继续。

</details>

#### NVMe

> 由于我们的设备不支持直接从 NVMe 驱动器启动，我们需要将 UEFI 安装到另一个介质。 在 UEFI 启动后，您可以直接从 NVMe 驱动器启动。 要将 UEFI 安装到您的 SPI 或 SD 卡，请遵循此指南。
> {.is-warning}

<details><summary><b>使用 USB 适配器</b></summary>

通过 USB 适配器将驱动器连接到您的电脑并继续 [**4.1 使用存储适配器**](#h-41-with-storage-adapter)。 刷写后将驱动器连接到您的 SBC 的 NVMe 端口。

</details>

<details><summary><b>没有适配器</b></summary>

将您的 NVMe 驱动器直接连接到您的 PC 并继续 [**4.1 使用存储适配器**](#h-41-with-storage-adapter)。 您可能必须强制您的刷写工具写入硬盘。

</details>

# 🚀 4. 刷写

> 我们提供了压缩为 .xz 文件的镜像。 请确保您在刷写之前解压它们！
> {.is-warning}

## 4.1 使用存储适配器

有无数工具可以刷写 SD 卡或 eMMC。 我们建议使用 `BalenaEtcher` 或 `Raspberry Pi Imager`。 这两个工具都支持 Linux、macOS 和 Microsoft Windows。

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

## 4.2 使用 RKDevelopTool

为了涵盖您可以为此使用的操作系统，我们决定将安装分成这两个指南：

- [在 Linux 或 macOS 下使用 RKDevelopTool 刷写](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [在 Microsoft Windows 下使用 RKDevelopTool 刷写](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
