---
title: 火箭驱动程序(主线Kernel)
description: 使用 BredOS 在Rockchip SOC上设置和使用神经处理股
published: false
date: 2026-03-19T13:28:53.204Z
tags:
editor: markdown
dateCreated: 2026-02-24T09：27：47.353Z
---

# 2. 介绍信息

一些Rockchip SoC公司包括一个专用神经处理股（“NPU”），以加快机器学习推断。 `RK3588`集成了6个TOPS NPU，拥有3个核心，能够运行定量的神经网络模型比CPU本身快得多。

由于内核`6.18`，Linux包含RK3588NPU的开源`Rocket`驱动程序。 在用户空间一侧，Mesa提供`Teflon`，TensorFlow Lite委托，向NPU硬件发送兼容的操作。 这两者结合在一起，允许在 BredOS 上运行 AI 推断，没有任何专利软件。

# 3. 支持的硬件

- 下表显示哪些Rockchip SoC包括一个由开放源码火箭驱动器支持的NPU：

| SoC                      | NPU Cores | 业绩    | 内核支持                  |
| ------------------------ | --------- | ----- | --------------------- |
| RK3588 / RK3588S         | 3         | 6 个主题 | 6.18+ |
| {.dense} |           |       |                       |

> 火箭驱动器目前只能支撑`RK3588`家庭。 计划向上游提供更多的Rockchip SOC支助。
> {.is-info}

所有带有`RK3588`或`RK3588S`的蓝牙支持板可以使用NPU。 This includes the Rock 5B, Rock 5B Plus, Orange Pi 5 series, and others listed on the [supported devices](/en/table-of-supported-devices) page.

# 4. 软件堆栈(开放源代码)

开源NPU堆栈有两个组件：

## 3.1 内核驱动程序(Rocket)

`Rocket`驱动程序是一个加速器驱动程序(`grav`子系统')，用于管理NPU硬件：启动/关闭，分配内存缓冲器和提交工作。 它暴露在`/dev/grad/redded0`上。

驱动程序是由 [Tomeu Vizoso](https://blog.tomeuvizoso.net/)开发的，并合并到 Linux `6.18` 主线。 BredOS 内核`6.18`，然后默认包括它。

## 3.2 用户空间(Mesa Teflon)

`Teflon`是包括在Mesa中的使用田间流利特的外部代表。 它通过火箭加里姆驱动程序将TFLite模型操作转换为NPU工作。

BredOS 飞船Mesa 使用 Teflon 内置支持。 委托书库位于`/usr/lib/libteflon.so`。

# 5. 设置

## 4.1 验证 Kernel 支持

- 检查`Rocket`模块是否已加载：

```
lsomd | grep 导弹
```

你应该在输出中看到`rocket`。 如果模块未加载，手动加载：

- 加载火箭模块：

```
Sudo modprobe导弹
```

- 验证 NPU 设备节点存在：

```
ls -l /dev/accel/accel0
```

> 如果`/dev/grad/redded0`不存在，您的内核可能会超过`6.18`或缺少`CONFIG_DRM_ACCEL_ROCKET` 选项。 更新到最近的 BredOS 内核。
> {.is-info}

## 4.2 安装用户空间包

NPU推断堆栈需要 Python 3.11`、`tflite-runtime`和`numpy`。 BredOS 目前将 Python `3.14` 作为系统默认值，但`tflite-runtime`仅提供最多为 Python`3.11\`的轮子。

- 安装 Python 3.11 和管道：

```
sudo pacman -S python311
```

- 安装 TFLite Runtime 和 Nump：

```
python3.11 -m pip install --user "numpy<2" tflite-runtime
```

> 需要`numpy<2` 约束，因为`tflite-runtime 2.14` 不兼容 NumPy 2.x。
> {.is-info}

- 可选，为图像预处理安装Pillow

```
python3.11 -m pip安装--user Pillow
```

## 4.3 验证Teflon 代表

- 确认`libteflon.so`是可用的：

```
ls /usr/lib/libteflon.so
```

如果文件丢失，更新Mesa：

- 将网格更新为带有Teflon 支持的版本：

```
sudo pacman -Syu mesa
```

# 4. 正在运行推文

本节展示在NPU上使用 MobileNet V1 进行图像分类。

## 5.1 下载模型和标签

- 下载数量化的移动网络V1模型和标签：

```
wget https://storage.googleapis.com/download.tensorflow.org/models/mobilenet_v1_2018_08_02/mobilenet_v1_1.0_224_quant.tgz
tar xzf mobilenet_v1_1.0_224_quant.tgz
wget storage.googleapis.com/download.tensorflow.org/models/mobilenet_v1_1.0_quant_and_labels.zip
unzip mobilenet_v1_1.0_224_quant_and_labels.zip
```

## 5.2 将图像分类

- 创建一个名为 `clasfy.py`的脚本：

```python
从 PIL 导入图像 A format@@1 导入np
为np 
 。 nterpreter as tflite

# Load Teflon 代表 for NPU size
representation = tflite. oad_delegate("/usr/lib/libteflon.so")
interpreter = tflite.Interpreter(
    model_path="mobilenet_v1_1. _224_quant.tflite",
    experimental_delegates=[delegate]

解释器。 llocate_tensors()

# 预处理图像
img = Image.open("your_image.jpg").重新大小(224, 224))
input_data = np.extend_dims(np. rray(img, dtype=np.uint8), axis=0)

# 运行inference
interpretter.set_tensor(interpretter.get_input_details()[0]["index"], input_data)
interpretter.invoicke()
output = inter.get_tensor(interpretter. et_output_details()[0]["index"])

# 显示顶级结果
打开("labels_mobilenet_quant_v1_224.txt") 为f:
    labels = f.read(). plitlines()
top = np.argmax(output[0])
print(f"预测：{labels[top]} ({output[0][top] / 255:.1%})")
```

- 使用 Python 3.11运行脚本

```
python3.11 classify.py
```

## 5.3 CPU 与 NPU 比较

要验证实际正在使用NPU，您可以在没有授权的情况下运行推断。

- 没有代表 (CPU 仅限) ，将翻译初始化更改为:

```python
解释器 = tflite.Interpreter(mel_path="mobilenet_v1_1.0_224_quant.tflite")
```

- 典型的 RK3588 和 MobileNet V1 量化比较：

| 方法                                       | 触发时间                   |
| ---------------------------------------- | ---------------------- |
| CPU (Cortex-A76)      | ~48 毫秒 |
| NPU (Teflon delegate) | ~13毫秒  |
| {.dense}                 |                        |

NPU为这一模型提供了大约3-4倍的加速。

# 🔄 3. 能力和限制

## 6.1 开放源码应用支持什么

火箭+Teflon堆栈支持在NPU上的下列TFLite操作：

- Convolutions (most configurs)
- 租户添加
- ReLU 激活 (与Convolume一起使用)
- 定量化(`uint8`) 模型

已成功测试的模型包括“MobileNetV1”、“MobileNetV2”和“MobileDet”。

## 6.2 开放源码头目前的限制

- **仅限定数量的模型** - NPU硬件使用固定点算术。 浮点型号完全在 CPU 上运行。
- **有限操作** - 只有潜入、添加和引爆的RELU卸载到NPU。 不支持的操作自动返回CPU。
- **没有高级活动** - 像SiLU (在YOLOv8中使用)这样的操作尚未实现。
- **单核执行** — 虽然RK3588拥有3个NPU核心，但当前驱动程序每次只使用一个核心。
- **CNN焦点** — 堆栈优化用于复杂神经网络。 基于转换的模型不会加速。
- **早期性能** - 开源堆栈在通过时与专有的 RKNN 驱动程序不匹配。

> 对于不支持的操作，Teflon 代表自动返回CPU，所以混合操作的模型仍将正确运行，只要部分加速。
> {.is-info}

# 9. 🤝 贡献

## 7.1 没有/dev/grad/grading 0

- 在内核中验证火箭模块可用：

```
zgrep CONFIG_DRM_ACCEL_ROCKET /proc/config.gz
```

输出应显示 `CONFIG_DRM_ACCEL_ROCKET=m` 或 `CONFIG_DRM_ACCEL_ROCKET=y`。 如果不是，你需要一个内核`6.18`，或此选项已启用。

## 7.2 Teflon 代表负载失败

- 检查使用Teflon 支持构建梅萨：

```
pacman -Ql mesa | grep teflon
```

如果`libteflon.so`未列出, 已安装的Mesa版本可能不包括 Teflon。 更新网格或检查 BredOS 仓库的更新包。

## 7.3 tflite-runtime 安装失败

如果“pip install tflite-runtime”失败，则使用“no match distribution”错误，请验证您正在使用 `Python 3.11`：

- 检查您的 Python 版本：

```
python3.11 --version
```

`tflite-runtime`软件包没有为所有Python版本提供轮子。 Python `3.11`是最新版本，并且已确认支持。

# 4. 参考

- [Rockchip NPU 更新 6: 我们是主线！](https://blog.tomeuvizoso.net/2025/07/rockchip-npu-update-6-we-are-in-mainline.html) - Tomeu Vizoso
- [grand/row火箭内核文档](https://docs.kernel.org/accel/rocket/index.html) - kernel.org
- [Collabora RK3588 mainline status](https://gitlab.collabora.com/hardware-enablement/rockchip-3588/notes-for-rockchip-3588/-/blob/main/mainline-status.md) - Collabora
- [在 Rockchip上运行主线Linux : 一年审查](https://www.collabora.com/news-and-blog/blog/2026/03/02/running-mainline-linux-u-boot-and-mesa-on-rockchip-a-year-in-review/) - Collabora (FOSDEM 2026)