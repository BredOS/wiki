---
title: 使用 Microsoft Windows 刷入 eMMC
description:
published: true
date: 2025-09-28T12:20:24.588Z
tags:
editor: markdown
dateCreated: 2025-09-16T09:55:34.272Z
---

# 1. 简介

首先，我们很抱歉听到您必须使用Windows。
但恐惧不是——我们还是看到了你了。
首先，我们很抱歉听到您必须使用Windows。
但恐惧不是——我们还是看到了你了。
首先，我们很抱歉听到您必须使用Windows。
但恐惧不是——我们还是看到了你了。
这篇文章引导您安装`RKDevTool` 和必要的`RockChip Maskrom drivers` 。

要安装BredOS，需要四件事：

1. SPI 加载器文件，例如 RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. 来自我们[官方网站]的设备特定图像(https://bredos.org/download.html)
3. [RockChip Maskrom drivers](https://dl.radxa.com/tools/windows/)
4. [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool), [替代链接 1](https://dl.radxa.com/tools/windows/)

> 我们以压缩文件提供我们的图像。 我们以压缩文件提供我们的图像。 您需要在刷入之前提取包含.img的文件！
> {.is-warning}
> {.is-warning}

# 2. 2. 驱动程序

我们从安装 [Rockchip 驱动器] (https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip )开始。 在你下载了那个.zip文件后，将其提取到你的预置位置。
你会在其中找到工具`DriverInstall.exe`。 使用更高的权限执行它。 在你下载了那个.zip文件后，将其提取到你的预置位置。
你会在其中找到工具`DriverInstall.exe`。 使用更高的权限执行它。 在你下载了那个.zip文件后，将其提取到你的预置位置。
你会在其中找到工具`DriverInstall.exe`。 使用更高的权限执行它。

> 如果您被问到：“您想要允许此应用更改您的设备吗？” ，点击“是”。
> {.is-info}
> {.is-info}
> {.is-info}

接着，一个窗口将响亮。 点击“安装驱动程序”。 然后将在您的系统上安装驱动程序。

# 3. 使用 RKDevTool 闪烁BredOS

有了驱动程序，我们可以继续使用 [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)。 解压缩.zip文件并执行 `RKDevTool.exe`。 解压缩.zip文件并执行 `RKDevTool.exe`。 解压缩.zip文件并执行 `RKDevTool.exe`。

在 `RKDevTool` 中，设置了以下配置并点击`RUN`：

- 选择与您的 SoC 对应的 SPI 加载文件
- 为您的 SBC 选择 BredOS 图像 (.img)
- 勾选 "Write by Address"
- 点击 `RUN`，等待进程完成

> Maskrom 按钮应该在电源插入棋盘时按住 \*\*。
> {.is-info}

> 使用USB-C到C电缆，或使用USB-C到电缆向后可能导致未被发现。
> 建议使用USB-C到A电缆， 然后是 [USB-C 女性到 USB-A 男性适配器](https://www.aliexpress.com/item/1005004767752226.html) 或 USB-A 到 A 电缆。
> {.is-warning}

等待它完成刷入过程，你很好。

> 在刷入成功后，继续进行 [**First Setup**](/en/install/first-setup)。
> {.is-success}
> {.is-success}
> {.is-success}