---
title: NPU
description: 使用 BredOS 在Rockchip SOC上设置和使用神经处理股
published: false
date: 2026-02-24T10:39:13.265Z
tags:
editor: markdown
dateCreated: 2026-02-18T09:54:15.539Z
---

# 2. 介绍信息

NPUs are specialized hardware accelerators designed to run AI inference workloads efficiently, delivering high performance with low power consumption. This enables running real-time tasks such as image recognition, object detection, and speech processing without relying on the cloud. RK35xx-based SoCs integrate a powerful on-chip NPU that brings AI performance to embedded platforms.

# 3. RKNN or Rocket driver, the differences

Currently, there are two drivers for RK3588 NPUs: the open-source Rocket driver and the proprietary RKNN driver. As of the time of writing, the Rocket driver does **not** support the NPU found on an RK3566. This may change in the near future.

## 2.1 RKNN driver

The RKNN driver is packaged with the BSP kernel 6.1. If you have the mainline kernel installed, you must use the Rocket driver or install the package `linux-rockchip-rk3` and boot this kernel instead.

Currently, the RKNN driver offers more support and better performance than the Rocket driver. However, as development of the Rocket driver continues, this will change in the future. Therefore, for long-term planning, we recommend using the Rocket driver.

> For more information about the RKNN driver have a look [here](/NPU/RKNN).
> {.is-info}

### 2.1.1 Supported Software

A wide range of software supports the RKNN driver out of the box. Below is a brief list of some examples:

- [Frigate](https://frigate.video/) (NVR-Software with AI-based detection of various objects)
- [Immich](https://immich.app/) (Photomanagment Software with AI-based sorting capabilities)
- [RKllama](https://github.com/NotPunchnox/rkllama) (Ollama alternative)

## 2.2 Rocket driver

The Rocket driver is installed by default starting from kernel version 6.18 onwards. Although it currently has limitations compared to the RKNN driver, its more standardized approach for implementing the NPU into the OS makes it more stable and future-proof than the outdated RKNN driver.

> For more information about the Rocket driver have a look [here](/NPU/rocket).
> {.is-info}

### 2.2.1 Supported Software

Since the Rocket driver utilizes standard protocols and device paths, it is already supported by several pieces of software.

\*[NPUs]: Neural Processing Units