---
title: RKNN driver (BSP Kernel)
description: 
published: false
date: 2026-03-19T13:28:51.474Z
tags: 
editor: markdown
dateCreated: 2026-02-24T09:28:20.286Z
---

# 1. Intoduction

# 2. Proprietary Stack (RKNN-Toolkit2)

## 2.1 Overview

Rockchip provides `RKNN-Toolkit2`, a proprietary SDK for NPU inference that supports significantly more operations and higher performance than the current open-source stack. It includes model conversion tools (ONNX, TensorFlow, PyTorch, TFLite to RKNN format), a C/C++ runtime library, and Python bindings.

## 2.2 Requirements

RKNN-Toolkit2 requires:

- A **BSP kernel** with the proprietary `rknpu.ko` driver (e.g., `linux-rockchip-rkr3` or `linux-rockchip-rkr6` packages on BredOS Legacy)
- The `rknpu2` userspace library from [rockchip-linux/rknpu2](https://github.com/rockchip-linux/rknpu2)

> On BredOS, the proprietary `rknpu.ko` driver is available on **Legacy** (BSP) images. If you are running a **Cutting Edge** (mainline) image, the open-source Rocket driver is used instead and RKNN-Toolkit2 will not work. Check your kernel track with `uname -r` — BSP kernels show versions like `6.1.x-rkrX-bredos`, while mainline kernels show `6.19.x-bredos` or `7.x`.
{.is-info}

## 2.3 Concrete Use Cases

The proprietary RKNN stack enables a much wider range of AI workloads than the open-source stack. Here are concrete use cases with software:

### Object Detection

| Project | Model | Performance | Link |
|---------|-------|-------------|------|
| rknn_model_zoo | YOLOv5, v8, v10, v11 | 50+ FPS (YOLOv8n) | [airockchip/rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo) |
| rknn-cpp-yolo | YOLOv11 + RGA preproc | 25 FPS (YOLOv11s) | [yuunnn-w/rknn-cpp-yolo](https://github.com/yuunnn-w/rknn-cpp-yolo) |
| YoloV5-NPU | YOLOv5/v6/v7/v8 | 53 FPS (YOLOv8n) | [Qengineering/YoloV5-NPU](https://github.com/Qengineering/YoloV5-NPU) |
| ros_rknn_yolo | YOLO as ROS node | Real-time | [BluewhaleRobot/ros_rknn_yolo](https://github.com/BluewhaleRobot/ros_rknn_yolo) |
{.dense}

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

| Use Case | Recommended Stack | BredOS Image |
|----------|-------------------|--------------|
| Simple CNN classification (MobileNet) | Rocket + Teflon (open-source) | Cutting Edge (mainline) |
| Object detection (YOLO) | RKNN-Toolkit2 | Legacy (BSP) |
| LLM inference on NPU | RKNN-LLM | Legacy (BSP) |
| Speech recognition | RKNN-Toolkit2 | Legacy (BSP) |
| Long-term mainline support | Rocket + Teflon (improving upstream) | Cutting Edge (mainline) |
{.dense}

> If you need maximum NPU performance or support for complex models (YOLO, LLMs, transformers), the RKNN-Toolkit2 with a vendor BSP kernel is currently the more capable option. The open-source Rocket + Teflon stack is actively improving and is the recommended long-term path for mainline kernel users.
{.is-info}

# 3. Troubleshooting

## 3.1 RKNN-Toolkit2 Does Not Work

RKNN-Toolkit2 requires the proprietary `rknpu.ko` driver, which is only available in BSP kernels. If you are running a BredOS **Cutting Edge** (mainline) image, switch to a **Legacy** (BSP) image or use the open-source Rocket + Teflon stack instead. See [section 7.2](#h-72-requirements).


# 4. References
- [RKNN-Toolkit2](https://github.com/airockchip/rknn-toolkit2) - Rockchip/Airockchip
- [RKNN-LLM](https://github.com/airockchip/rknn-llm) - Rockchip/Airockchip (LLM inference on NPU)
- [RKNN Model Zoo](https://github.com/airockchip/rknn_model_zoo) - Rockchip/Airockchip (official demos and benchmarks)
- [rknpu2 userspace library](https://github.com/rockchip-linux/rknpu2) - Rockchip