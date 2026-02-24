---
title: NPU
description: 使用 BredOS 在Rockchip SOC上设置和使用神经处理股
published: false
date: 2026-02-24T19：46：29.573Z
tags:
editor: markdown
dateCreated: 2026-02-18T09:54:15.539Z
---

# 2. 介绍信息

NPU是专用硬件加速器，旨在高效运行 AI 推导负荷，提供低耗电的高性能。 这使得能够运行图像识别、对象检测和语音处理等实时任务，而不依赖云。 基于 RK35xx的 SoCs 集成了一个强大的芯片NPU，它为嵌入式平台提供了AI 性能。

# 3. RKNN 或 火箭驱动器的差异

目前，RK3588NPU有两个驱动程序：开放源码火箭驱动程序和专有的RKN驱动程序。 截至撰写本报告时，火箭驱动程序**不** 支持RK3566上发现的NPU。 这种情况在不久的将来可能会改变。

## 2.1 RKNN 驱动

RKNN 驱动程序被打包使用 BSP 内核6.1。 如果你安装了主线内核，你必须使用火箭驱动程序或安装软件包 `linux-rockchip-rkr3` 然后启动这个内核。

目前，RKN驾驶员提供的支持和性能优于火箭驱动器。 然而，随着火箭驾驶员的发展继续，这种情况今后将会改变。 因此，为了进行长期规划，我们建议使用火箭驱动器。

> 关于RKNN驱动程序的更多信息有一个外观 [here](/NPU/RKNN)。
> {.is-info}

### 2.1.1 支持的软件

一系列广泛的软件支持RKN驱动程序出箱。 以下是一些例子的简要清单：

- [Frigate](https://frigate.video/(NVR-Software with AI检测到各种对象)
- [Immich](https://immich.app/) (带有基于 AI的排序能力的霍特制软件)
- [RKllama](https://github.com/NotPunchnox/rkllama) (替代)

## 2.2 火箭驱动程序

火箭驱动程序默认从内核版本6.18起安装。 尽管它目前与RKN驱动程序相比有局限性， 它在操作系统中安装NPU的更标准化的方法使它比过时的 RKNN 驱动程序更加稳定和有前途。

> 关于火箭驱动程序的更多信息有一个外观 [here](/NPU/rocket)。
> {.is-info}

### 2.2.1 支持的软件

由于火箭驱动程序使用标准协议和设备路径，它已经得到几个软件的支持。

\*[NPUs]: 神经处理股