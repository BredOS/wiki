---
title: Radxa Orion O6
description:
published: false
date: 2025-09-17T14：18：07.677Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. 简介

Orion O6是一个 ITX-formed ARM64 型号的面板，具有很强的特性：

- SoC：CIX CD8180
- CPU： 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
- GPU： 不稳定的 G720 MC10
- NPU： 30 TOPs
- 网络：2x 5Gbit 以太网 (PCIe 4.0 每个路由)

PCIe 端口：

- M.2 M 密钥 (PCIe 4.0 4x 通道)
- M.2 E key (PCIe 4.0 2.x 通道)
- 全尺寸的 PCIe x16 槽(PCIe 4.0 8x 长道)

> 我们因为Pandas打字技能而把它命名为“_普里昂_”。
> {.is-info}

# 2. 下载

您可以在我们的 [Github 页面] (https://github.com/BredOS/bredos-iso/releases/latest )中找到无主文件的下载链接！

我们有两个版本：一个基于Radxa的6.6内核，另一个基于主线。
基于6.6内核的版本包含"ORION"的名称，支持该棋盘的完整功能。
主行内核确实缺少驱动程序。 在主线上工作的概述和whats无法在第4节下找到。 Mainline support\`.

# 3. 安装

Prion支持使用通用的 ISO 图像进行安装，不像我们其他支持的单板计算机（SBCs），后者使用设备特定图像。 安装可以使用 USB 棍棒，甚至使用 USB 光学驱动器。

## 3.1 通用ISO 安装

通用.iso安装指南可用 [here](/en/install/Installation-with-ISO)。

## 3.2 UEFI 安装

我们已经根据Radxa's source 代码开发了一个自定义 UEFI。 它支持出售棋盘的实际CPU速度， 允许控制 PCIe 链接速度，并且——最好的 - 启动时显示 Bred 徽标。 更新您的 UEFI 的完整功能列表和指南是可用的 [here](/en/radxa-orion-o6/prion-uefi-installation)。

# 4. 主线支持

| `linux`                 | 状态  | 注意                                                              |
| ----------------------- | --- | --------------------------------------------------------------- |
| 主线                      | 工作  |                                                                 |
| CPU                     | 工作  |                                                                 |
| RAM                     | 工作  |                                                                 |
| GPU                     | 断开  | 没有驱动程序                                                          |
| NPU                     | 断开  | 没有驱动程序                                                          |
| 硬件编码                    | 断开  | 没有驱动程序                                                          |
| 硬件解码                    | 断开  | 没有驱动程序                                                          |
| HDMI                    | 部分的 | EFI FB 局部工作 (1080P@60Hz 大部分显示器) |
| 潜行者                     | 部分的 | 与上面相同                                                           |
| USB-C DP                | 部分的 | 与上面相同                                                           |
| 存储                      | 工作  | M.2 SSD按预期工作                                    |
| 以太网                     | 工作  |                                                                 |
| 前方USB                   | 工作  | 随机死亡, 需要自定义的 BredOS 派生Radxa bios                                |
| 后方USB                   | 工作  | 随机死亡, 需要自定义的 BredOS 派生Radxa bios                                |
| 前置音频                    | 断开  | 没有驱动程序                                                          |
| 后端音频                    | 断开  | 没有驱动程序                                                          |
| RTC                     | 工作  | 没有驱动程序                                                          |
| UART                    | 工作  | 开机时`ttyS2`                                                      |
| PCIe                    | 部分的 | 适合大多数设备，但某些GPU无法正常工作。 <br> 有时冻结整个系统。 考虑使用我们的偏差。                 |
| M.2 E 键 | 工作  |                                                                 |
| M.2M 键  | 工作  |                                                                 |
| 风扇控制                    | 工作  | 自动粉丝控制，不能控制操作系统                                                 |

# 5. PCIe

一些测试者发现，当使用PCIe Gen4速度运行的设备连接时，该系统变得不稳定。 如果你的棋盘不稳定，请考虑更新到我们的 UEFI 固件并设置链接速度到 3 基因。