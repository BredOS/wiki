---
title: 橙色Pi 6 +
description:
published: true
date: 2025-11-24T07：15：03.864Z
tags:
editor: markdown
dateCreated: 2025-11-24T07：14：51.932Z
---

# 2. 介绍信息

Orange Pi 6 Plus是一个ARM64板，具有很高的规格：

- SoC：CIX CD8160
- CPU： 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
- GPU： 不稳定的 G720 MC10
- NPU： 28.8 Tops
- 网络：2x 5Gbit 以太网 (PCIe 4.0 每个路由)

PCIe 端口：

- 2x M.2 M 键 (PCIe 4.0 4x 通道)
- 1x M.2 E 键 (PCIe 4.0 2x 通道)

> 我们把它命名为“_阿片6plus_”。
> {.is-info}

# 3. 刷入

您可以在我们的 [Github 页面] (https://github.com/BredOS/bredos-iso/releases/latest )中找到无主文件的下载链接！

目前我们提供一个基于主线内核的图像。 此版本确实缺少驱动程序。 在主线上工作的概述和whats 找不到[4]。 主线支持](#h-4-mainline-support)。

# 4. 安装 rkdeveloptool

阿片6plus支持来自通用ISO图像的安装，不像我们其他支持的单板计算机（SBCs），后者使用设备特定图像。 安装可以使用 USB 棍棒，甚至使用 USB 光学驱动器。

## 3.1 通用ISO 安装

通用.iso安装指南可用 [here](/en/install/Installation-with-ISO)。

# 5. PCIe

| `linux`                 | 状态  | 注释                                                                                  |
| ----------------------- | --- | ----------------------------------------------------------------------------------- |
| CPU                     | 工作  |                                                                                     |
| RAM                     | 工作  |                                                                                     |
| GPU                     | 断开  | 潜行者                                                                                 |
| NPU                     | 断开  | 潜行者                                                                                 |
| 硬件编码                    | 断开  | 潜行者                                                                                 |
| 硬件编码                    | 断开  | 潜行者                                                                                 |
| HDMI                    | 部分的 | EFI FB 局部工作 (1080P@60Hz 大部分监视器) / 4K 监视器在UEFI 期间不工作 |
| 潜行者                     | 部分的 | 木头很好                                                                                |
| USB-C DP                | 部分的 | UEFI时没有输出                                                                           |
| 存储                      | 工作  | M.2 SSD按预期工作                                                        |
| 以太网                     | 工作  |                                                                                     |
| 后方USB                   | 工作  |                                                                                     |
| 前方USB                   | 工作  |                                                                                     |
| 后端音频                    | 断开  | 潜行者                                                                                 |
| 前置音频                    | 断开  | 潜行者                                                                                 |
| RTC                     | 工作  | 潜行者                                                                                 |
| UART                    | 工作  | 开机时`ttyS2`                                                                          |
| PCIe 稳定性                | 工作  | 正常工作                                                                                |
| M.2M 键  | 工作  |                                                                                     |
| M.2 E 键 | 工作  |                                                                                     |
| 风扇控制                    | 工作  | 自动粉丝控制，不能控制操作系统                                                                     |
