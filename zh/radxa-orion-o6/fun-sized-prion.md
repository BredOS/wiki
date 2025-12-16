---
title: Radxa Orion O6N
description:
published: true
date: 2025-12-16T10:50:13.899Z
tags:
editor: markdown
dateCreated: 2025-12-15T09：55：40.646Z
---

# 2. 介绍信息

Orion O6是一个Nano ITX格式的ARM64牌，具有很高的规格：

- SoC：CIX CD8180
- CPU： 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
- GPU： 不稳定的 G720 MC10
- NPU： 30 TOPs
- 网络：2x 2.5Gbit 以太网 (每条PCIe 4.0 1.x 通道)

PCIe 端口：

- 2x M.2 M 键 (PCIe 4.0 4x 通道)
- M.2 E key (PCIe 4.0 2.x 通道)
- M.2 B key (PCIe 4.0 2.x 通道)

> 我们把它命名为“\*有趣的狮子”，因为它像的 [Prion](/en/radxa-orion-o6/prion)，但很有趣。
> {.is-info}

# 3. 刷入

您可以在我们的 [Github 页面] (https://github.com/BredOS/bredos-iso/releases/latest )中找到无主文件的下载链接！

# 4. 安装 rkdeveloptool

有趣的 Prion 支持使用通用的 ISO 图像进行安装，不像我们所支持的使用设备特定图像的单板计算机(SBC)。 安装可以使用 USB 棍棒，甚至使用 USB 光学驱动器。

## 3.1 通用ISO 安装

通用.iso安装指南可用 [here](/en/install/Installation-with-ISO)。

# 5. PCIe

| `linux`                                             | 状态  | 注释                                                              |
| --------------------------------------------------- | --- | --------------------------------------------------------------- |
| CPU                                                 | 工作  |                                                                 |
| RAM                                                 | 工作  |                                                                 |
| GPU                                                 | 断开  | 潜行者                                                             |
| NPU                                                 | 断开  | 潜行者                                                             |
| 硬件编码                                                | 断开  | 潜行者                                                             |
| 硬件编码                                                | 断开  | 潜行者                                                             |
| HDMI                                                | 部分的 | EFI FB 局部工作 (1080P@60Hz 大部分显示器) |
| 潜行者                                                 | 部分的 | 与上面相同                                                           |
| USB-C DP                                            | 部分的 | 与上面相同                                                           |
| 存储                                                  | 工作  | M.2 SSD按预期工作                                    |
| 以太网                                                 | 工作  |                                                                 |
| 后方USB                                               | 工作  | 随机死亡, 需要自定义的 BredOS 派生Radxa bios                                |
| 前方USB                                               | 工作  | 随机死亡数                                                           |
| 后端音频                                                | 断开  | 潜行者                                                             |
| 前置音频                                                | 断开  | 潜行者                                                             |
| RTC                                                 | 工作  | 潜行者                                                             |
| UART                                                | 工作  | 开机时`ttyS2`                                                      |
| PCIe (任何 M.2 端口) | 部分的 | 对大多数设备都很好，但是某些GPU不能按预期运行，并且有时冻结整个系统。 见**5。 PCIe**               |
| M.2M 键                              | 工作  |                                                                 |
| M.2 E 键                             | 工作  |                                                                 |
| M.2 B 键                             | 工作  |                                                                 |
| 风扇控制                                                | 工作  | 自动粉丝控制，不能控制操作系统                                                 |

# 🔄 3. PCIe 稳定性

一些测试者发现，当使用PCIe Gen4速度运行的设备连接时，该系统变得不稳定。 一些测试者发现，当使用PCIe Gen4速度运行的设备连接时，该系统变得不稳定。 如果你的棋盘不稳定，请考虑更新到我们的 UEFI 固件并设置链接速度到 3 基因。 一些测试者发现，当使用PCIe Gen4速度运行的设备连接时，该系统变得不稳定。 如果你的棋盘不稳定，请考虑更新到我们的 UEFI 固件并设置链接速度到 3 基因。 如果你的棋盘不稳定，请考虑设置链接速度到Gen3。