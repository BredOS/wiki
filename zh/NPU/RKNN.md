---
title: RKNN 驱动程序(BSP Kernel)
description:
published: false
date: 2026-03-19T13：28：51.474Z
tags:
editor: markdown
dateCreated: 2026-02-24T09:28:20.286Z
---

# 2. 上岗培训

# 3. 专有堆栈(RKNN-Toolkit2)

## 2.1 概览

Rockchip 提供 `RKNN-Toolkit2` ，一个NPU 内推的专有的 SDK 支持比当前开源堆栈高得多的操作和性能。 它包括模型转换工具 (ONX, TensorFlow, PyTorch, TFLite to RKNN 格式), C/C++ 运行时库和 Python 绑定。

## 2.2 所需经费

RKNN-Toolkit2 需要：

- 一个 **BSP 内核** 和专有的 `rknpu.ko` 驱动程序（如：`linux-rockchip-rkr3` 或 `linux-rockchip-rkr6` 包在 BredOS Legacy上）
- The `rknpu2` userspace library from [rockchip-linux/rknpu2](https://github.com/rockchip-linux/rknpu2)

> 在 BredOS, 专有的 `rknpu.ko` 驱动程序在 **Legacy** (BSP) 图像上可用。 如果您正在运行一个 **剪切边** (主线) 图像，则使用开源火箭驱动程序，RKNN Toolkit2 将无法工作。 使用"uname -r"检查您的内核轨迹-BSP 内核显示类似于"6.1.x-rkrX-bredos"的版本，而主内核则显示"6.19.x-bredos"或"7.x"。
> {.is-info}

## 2.3 具体使用案件

专有的 RKNN 堆栈比开源堆放更广泛的 AI 工作负荷。 以下是使用软件的具体实例：

### 对象检测

| 项目                                                       | 模型                    | 业绩                                   | 链接                                                                                                                        |
| -------------------------------------------------------- | --------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| rknn_model_zoo | YOLOv5, v8, v10, v11  | 50+ FPS (YOLOV8n) | [airockchip/rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo)       |
| rknn-cpp-yolo                                            | YOLOv11 + RGA preproc | 25 FPS (YOLOv11s) | [yuunnn-w/rknn-cpp-yolo](https://github.com/yuunnn-w/rknn-cpp-yolo)                                                       |
| YoloV5-NPU                                               | YOLOv5/v6/v7/v8       | 53 FPS (YOLOv8n)  | [Qengineering/YoloV5-NPU](https://github.com/Qengineering/YoloV5-NPU)                                                     |
| ros_rknn_yolo  | YOLO 作为ROS节点          | 实际时间                                 | [BluewhaleRobot/ros_rknn_yolo](https://github.com/BluewhaleRobot/ros_rknn_yolo) |
| {.dense}                                 |                       |                                      |                                                                                                                           |

### LLM and Multimodal Inference

Rockchip 提供 [rknn-llm](https://github.com/airockchip/rknn-llm，一个用于在NPU上运行大型语言模型和视觉语言模型的专用工具包：

- **Qwen2-VL**：完全在NPU上运行的多式联运视觉语言模型
- **DeepSeek-R1-Distill-Qwen-1.5B**：精炼推理模型
- **rkllm_server**：LLM 内嵌本地API服务器
- **多式对话**：交互式文本+图像对话

### 语音和音频

[rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo):

- **Whisper**: speeching to text translation
- **Zipformer**：流媒体语音识别
- **MMS-TTS**：文本到语音合成。
- **Wav2Vec**：语音演示学习
- **YamNet**：音频事件分类

### 其他视觉任务

- **RetinaFace**：面部检测(243 FPS 带有mobile320 模式)
- **MobileSAM**：边缘设备上的任何片段
- **CLIP**：图像文本匹配和零截图分类
- **PPOCR**：文本检测和识别 (OCR)
- **YOLOv8-pose**：人类的估计值
- **YOLOv8-OBB**：定向边界框检测

## 2.4 何时使用哪个应用

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

# 3. 🤝 贡献

## 3.1 RKNN-工具包2 不工作

RKNN-Toolkit2 需要专有的 `rknpu.ko` 驱动器，这只能在 BSP 内核中使用。 如果您正在运行 BredOS **剪切边** (主线) 图像，请切换到 **Legacy** (BSP) 图像或使用开源火箭+Teflon 堆栈。 See [section 7.2](#h-72-requirements).

# 5. 参考

- [RKNN-Toolkit2](https://github.com/airockchip/rknn-toolkit2) - Rockchip/Airockchip
- [RKNN-LLM](https://github.com/airockchip/rknn-llm) - Rockchip/Airockchip (LLM inference on NPU)
- [RKNN 模型动物园](https://github.com/airockchip/rknn_model_zoo) - Rockchip/Airockchip (官方演示和基准)
- [rknpu2 用户空间库](https://github.com/rockchip-linux/rknpu2) - Rockchip