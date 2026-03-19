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
| ros_rknn_yolo  | YOLO as ROS node      | Real-time                            | [BluewhaleRobot/ros_rknn_yolo](https://github.com/BluewhaleRobot/ros_rknn_yolo) |
| {.dense}                                 |                       |                                      |                                                                                                                           |

### LLM and Multimodal Inference

Rockchip provides [rknn-llm](https://github.com/airockchip/rknn-llm), a dedicated toolkit for running large language models and vision-language models on the NPU:

- **Qwen2-VL**: multimodal vision-language model running entirely on NPU
- **DeepSeek-R1-Distill-Qwen-1.5B**: distilled reasoning model
- **rkllm_server**: local API server for LLM inference
- **Multimodal dialogue**: interactive text+image conversations

### Speech and Audio

Available in [rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo):

- **Whisper**: speech-to-text transcription
- **Zipformer**: streaming speech recognition
- **MMS-TTS**: text-to-speech synthesis
- **Wav2Vec**: speech representation learning
- **YamNet**: audio event classification

### Other Vision Tasks

- **RetinaFace**: face detection (243 FPS with mobile320 model)
- **MobileSAM**: segment-anything on edge devices
- **CLIP**: image-text matching and zero-shot classification
- **PPOCR**: text detection and recognition (OCR)
- **YOLOv8-Pose**: human pose estimation
- **YOLOv8-OBB**: oriented bounding box detection

## 2.4 When to Use Which Stack

| Use Case                                                 | Recommended Stack                                       | BredOS Image                               |
| -------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------ |
| Simple CNN classification (MobileNet) | Rocket + Teflon (open-source)        | Cutting Edge (mainline) |
| Object detection (YOLO)               | RKNN-Toolkit2                                           | Legacy (BSP)            |
| LLM inference on NPU                                     | RKNN-LLM                                                | Legacy (BSP)            |
| Speech recognition                                       | RKNN-Toolkit2                                           | Legacy (BSP)            |
| Long-term mainline support                               | Rocket + Teflon (improving upstream) | Cutting Edge (mainline) |
| {.dense}                                 |                                                         |                                            |

> If you need maximum NPU performance or support for complex models (YOLO, LLMs, transformers), the RKNN-Toolkit2 with a vendor BSP kernel is currently the more capable option. The open-source Rocket + Teflon stack is actively improving and is the recommended long-term path for mainline kernel users.
> {.is-info}

# 3. 🤝 贡献

## 3.1 RKNN-Toolkit2 Does Not Work

RKNN-Toolkit2 requires the proprietary `rknpu.ko` driver, which is only available in BSP kernels. If you are running a BredOS **Cutting Edge** (mainline) image, switch to a **Legacy** (BSP) image or use the open-source Rocket + Teflon stack instead. See [section 7.2](#h-72-requirements).

# 5. References

- [RKNN-Toolkit2](https://github.com/airockchip/rknn-toolkit2) - Rockchip/Airockchip
- [RKNN-LLM](https://github.com/airockchip/rknn-llm) - Rockchip/Airockchip (LLM inference on NPU)
- [RKNN Model Zoo](https://github.com/airockchip/rknn_model_zoo) - Rockchip/Airockchip (official demos and benchmarks)
- [rknpu2 userspace library](https://github.com/rockchip-linux/rknpu2) - Rockchip