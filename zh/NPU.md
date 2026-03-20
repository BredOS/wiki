---
title: NPU
description: 使用 BredOS 在Rockchip SOC上设置和使用神经处理股
published: true
date: 2026-03-20T09：09：08.606Z
tags: npu, rk3588, ai, 机器学习
editor: markdown
dateCreated: 2026-02-18T09:54:15.539Z
---

# 2. 介绍信息

一些Rockchip SoC公司包括一个专用神经处理股（“NPU”），以加快机器学习推断。 `RK3588`集成了6个TOPS NPU，拥有3个核心，能够运行定量的神经网络模型比CPU本身快得多。

RK3588NPU有**两个单独的软件堆栈**，每个堆栈都有不同的内核要求：

| 堆栈... | 内核数                            | 许可协议      | 能力                                                              |
| ----------------------------------------------------- | ------------------------------ | --------- | --------------------------------------------------------------- |
| **火箭+Teflon** (开源)                 | Mainline 6.18+ | GPL / MIT | TFLite quantized CNN inference (limited ops) |
| **RKNN Toolkit2** (专有)             | 仅限供货商 BSP                      | 专有性       | 全部推论：YOLO、LLM、演讲、多式联赛                                           |
| {.dense}                              |                                |           |                                                                 |

> BredOS 提供两个内核轨迹：**剪切边** (主线) 和 **Legacy** (Rockchip BSP)。 开源火箭+Teflon堆栈用于剪切边缘内核6.18及以后的工作。 专有的 RKNN Toolkit2 需要 **BSP 内核** 并在 BredOS **Legacy** 图像上工作。 请注意，切割边缘(主线)图像目前仅适用于少数看板——大多数看板默认带有旧图像。
> {.is-info}

# 3. 堆栈之间的差异

## 2.1 何时使用哪个应用

- 下表简要概述了何时使用哪个堆栈：

| 使用大小写                                     | 推荐应用                                | BredOS 图像                   |
| ----------------------------------------- | ----------------------------------- | --------------------------- |
| 简单的 CNN 分类 (MobileNet) | 火箭+Teflon (开源)   | 剪切边缘(主线) |
| 对象检测 (YOLO)            | RKNN-工具包2                           | 传统(BSP)  |
| NPU上的 LLM 推文                              | RKNN-LLM                            | 传统(BSP)  |
| 语音识别                                      | RKNN-工具包2                           | 传统(BSP)  |
| 长期主线支持                                    | 火箭+Teflon (改进上游) | 剪切边缘(主线) |
| {.dense}                  |                                     |                             |

> 如果您需要最大的NPU性能或对复杂模型的支持(YOLO, LLMs, 变压器) 带有供应商BSP 内核的 RKNN-Toolkit2 目前是更具能力的选项。 开源火箭+Teflon堆栈正在积极改进，是主线内核用户推荐的长期路径。
> {.is-info}

## 2.2 进一步资料

要找到如何使用您芯片的 NPU 的更多信息，请根据您的驱动程序参考该文章。

- For BSP (Legacy) [click here](/NPU/RKNN).
- For Mainline (cutting edge) [click here](/en/NPU/rocket).
