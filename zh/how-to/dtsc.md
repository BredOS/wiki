---
title: DTSC 助手脚本
description: 使用 BredOS 设备树源编译器助手脚本
published: true
date: 2025-05-07T13:40:24.351Z
tags: null
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# DTSC 助手脚本

`dtsc` 是一个默认与 BredOS 和 `bredos-tools` 软件包一起提供的命令。
但要让它起作用，你需要安装 `dtc`，只需运行 `yay -S dtc`

脚本是一个 dtc 的包装器，执行自动的 gcc 预处理、链接和生成所需文件。
它使得设备树的生成和测试大为简化。
它自动决定并生成基础设备树或叠加层。

## 重要说明

**在您的设备上安装不正确的设备树将使它无法操作。**
**小心，执行备份并确保一个应急计划。**

# 用法

```
用法：dtsc [-h] [-o OUTPUT] [-i INCLUDE] [-k KERNEL] [input]

将一个设备树源(DTS) 文件编译成一个设备树二进制文件(DTBO 或 DTB)。

位置参数：
  input                 输入 DTS 文件

选项：
  -h, --help            显示此帮助消息并退出
  -o, --output OUTPUT   输出文件(默认：生成匹配输入文件名的 .dtb)
  -i, --include INCLUDE 附加设备树文件(可选)
  -k, --kernel KERNEL   手动指定内核源路径 (默认：自动检测)

示例：dtsc my_device_tree.dts -o output.dtbo
```

## 输入

脚本需要输入 `.dts` 文件。如果没有指定输出，它生成匹配名称的 `.dtb` 文件。
输出文件名可以用 `-o` 参数设置。

## 与内核链接

如果您有多个内核安装在您的系统上，您应该指定要链接的内核路径。
它应该看起来像这样：

```
dtsc example.dts -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

如果您安装了单个内核，这将自动被检测。

## 编译基础设备树

如果您正在编译基础设备树而不是叠加层，您将需要您的内核全部源码，这些源码没有预装。
这是因为这些树需要包含其他 ".dtsi" 设备树。

要编译这样一个设备树，请使用 git 克隆你的内核存储库到已知路径。

`linux-rockchip-rkr3` 内核的示例：

```
git clone https://github.com/BredOS/linux-bredos
```

然后按您想要的方式运行 dtsc，但使用 "-i" 标志指定它想要链接的文件夹。

例如，假定我们想要编译一个 rk3588 开发板的设备树，我们需要指定以下选项：

```
dtsc rk3588-exampleboard.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-exampleboard.dtb
```