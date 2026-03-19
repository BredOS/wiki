---
title: NPU
description: Setting up and using the Neural Processing Unit on Rockchip SoCs with BredOS
published: false
date: 2026-03-19T13:28:49.879Z
tags: npu, rk3588, ai, machine-learning
editor: markdown
dateCreated: 2026-02-18T09:54:15.539Z
---

# 1. Introduction

Some Rockchip SoCs include a dedicated Neural Processing Unit (`NPU`) designed to accelerate machine learning inference. The `RK3588` integrates a 6 TOPS NPU with 3 cores, capable of running quantized neural network models significantly faster than the CPU alone.

There are **two separate software stacks** for the RK3588 NPU, each with different kernel requirements:

| Stack | Kernel | License | Capabilities |
|-------|--------|---------|-------------|
| **Rocket + Teflon** (open-source) | Mainline 6.18+ | GPL / MIT | TFLite quantized CNN inference (limited ops) |
| **RKNN-Toolkit2** (proprietary) | Vendor BSP only | Proprietary | Full inference: YOLO, LLM, speech, multimodal |
{.dense}

> BredOS provides two kernel tracks: **Cutting Edge** (mainline) and **Legacy** (Rockchip BSP). The open-source Rocket + Teflon stack works on Cutting Edge kernels 6.18 and later. The proprietary RKNN-Toolkit2 requires a **BSP kernel** and works on BredOS **Legacy** images. Note that Cutting Edge (mainline) images are currently available only for a handful of boards — most boards ship with Legacy images by default. 
{.is-info}

# 2. Further Information
To find futher information on how to use the NPU of your Board refer to the article according to your driver.

- For BSP (Legacy) [click here](/NPU/RKNN).
- For Mainline (cutting edge) [click here](/en/NPU/rocket).
