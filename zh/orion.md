---
title: Radxa Orion系列
description:
published: false
date: 2025-09-17T00：08：50.283Z
tags:
editor: markdown
dateCreated: 2025-09-17T00：08：50.283Z
---

# 简介

SoC：CIX CD8180
CPU：4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1。 GHz
GPU: Immortals G720 MC10
NPU: 30 TOPs
Network: 2x 5Gbit 以太网 (PCIe 4.0 1.x 每个航道)
PCI:

- M.2 M 密钥 (PCIe 4.0 4x 通道)
- M.2 E key (PCIe 4.0 2.x 通道)
- 全尺寸的 PCIe x16 槽(PCIe 4.0 8x 长道)

# 主线支持

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
| PCIe                    | 部分的 | 适合大多数设备，但某些GPU无法正常工作。 <br> 有时冻结整个系统 <br> 有时冻结整个系统 <br> 有时冻结整个系统 |
| M.2 E 键 | 工作  |                                                                 |
| M.2M 键  | 工作  |                                                                 |
| 风扇控制                    | 工作  | 自动粉丝控制，不能控制操作系统                                                 |