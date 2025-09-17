---
title: Radxa Orion O6
description:
published: false
date: 2025-09-17T08:50:00.224Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. 简介

Radxa Orion O6是一个小型ITX母板，由Cix P1(CD8180)SOC驱动，它拥有一个 12colcore ARM v9。 CPU 拥有4个大CortexcutA720核心(~2.8GHz)，4个中等A720s (~2.4GHz)，4个小CortexhopA520s (~1.8GHz)。  它包括一个军火不稳定G720 GPU和一个用于大赦国际推断的30个TOPS NPU。  拥有多达64GB LPDDR5，多个显示输出结果，双倍5GbE 网络和PCIe Gen 4扩展， 它针对edge AI, multimedia和开发者工作站应用程序。

> 我们因为Pandas打字技能而把它命名为“_普里昂_”。
> {.is-info}

# 2. 下载

您可以在我们的 [Github 页面] (https://github.com/BredOS/bredos-iso/releases/latest )中找到无主文件的下载链接！

我们有两个版本：一个基于Radxa的6.6内核，另一个基于主线。 基于6.6内核的版本包含"ORION"的名称，支持该棋盘的完整功能。 主行内核确实缺少驱动程序。 在主线和whats上运行的很好的概述无法找到 [here](/en/table-of-supported-devices)。

# 3. 安装

Prion支持使用通用的 ISO 图像进行安装，不像我们其他支持的单板计算机（SBCs），后者使用设备特定图像。 安装可以使用 USB 棍棒，甚至使用 USB 光学驱动器。

## 3.1 通用ISO 安装

通用.iso安装指南在此可用。

## 3.2 UEFI 安装

我们已经根据Radxa's source 代码开发了一个自定义 UEFI。 它支持出售棋盘的实际CPU速度， 允许控制 PCIe 链接速度，并且——最好的 - 启动时显示 Bred 徽标。 更新您的 UEFI 指南是可用的 [here](/en/radxa-orion-o6/prion-uefi-installation)。

# 4. PCIe

一些测试者发现，当使用PCIe Gen4速度运行的设备连接时，该系统变得不稳定。 如果你的棋盘不稳定，请考虑更新到我们的 UEFI 固件并设置链接速度到 3 基因。