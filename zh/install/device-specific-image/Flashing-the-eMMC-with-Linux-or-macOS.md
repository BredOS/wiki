---
title: 使用 Linux 或 macOS 刷入 eMMC
description:
published: false
date: 2025-09-18T08:57:18.967Z
tags:
editor: markdown
dateCreated: 2025-09-16T06:29:26.865Z
---

# 1. 简介

本指南描述如何使用 rkdeveloped tool\\\` 工具刷入eMC。 它可以在 Linux 仓库中找到，也可以在 macOS 上运行。 它可以在 Linux 仓库中找到，也可以在 macOS 上运行。 它可以在 Linux 仓库中找到，也可以在 macOS 上运行。

要安装BredOS，需要三件事：

1. SPI 加载器文件，例如 RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. 来自我们[官方网站]的设备特定图像(https://bredos.org/download.html)
3. `rkdevelopmenttool`

# 3) 刷入

可以通过以下步骤安装 `rkdeveloptool` 。

## 2.1 Linux

- 如果您正在使用基于归档的分布

```
sudo pacman -S rkdeveloptool
```

- 如果您正在使用基于 Debian的分布

```
sudo apt install rkdeveloped tools
```

- 如果您正在使用红帽子分布

```
sudo dnf install rkdeveloped tools
```

## 2.2 macOS

### 2.2.1 前提条件

由于没有用于 macOS 的 "rkdeveloped tool" 的二进制包，我们需要自己编译它。 为了做到这一点，我们需要通过 [Brew](https://brew.sh/)安装一些软件包。 为了做到这一点，我们需要通过 [Brew](https://brew.sh/)安装一些软件包。 为了做到这一点，我们需要通过 [Brew](https://brew.sh/)安装一些软件包。

- 安装`autocake`、`autocconf`、`libbus`、`pkg-config`、`git`和\`wget\`\\\` ，具有以下命令：

```
brew install automake autoconf libusb pkg-config git wget
```

### 2.2.2 克隆仓库

- 获取源代码：

```
git clone https://github.com/rockchip-linux/rkdevelopmenttools
```

### 2.2.3 编译为二进制文件

- 现在更改到包含源代码的目录并遵守它：

```
cd rkdeveloptool
autoreconf -i
./configure
make -j $(nproc)
```

- 在进程 `make` 完成后没有任何错误，在您当前的文件夹中有文件 `rkdevelopmenttool` ：

```
ls | grep rkdeveloping 工具
```

- 应该输出

```
rkdeveloped 工具
```

### 2.2.4 使其运行

- 最后复制它到`opt`文件夹，然后从任何地方运行它：

```
cp rkdevelopmenttool/opt/homebrew/bin/
```

# 3. 刷入

## 3.1 输入掩码

要使SBC 在USB上显示为易燃设备，它需要设置为 \\\`maskrom 模式'。 这可以根据您正在使用的设备来实现。 有些SBC有一个按钮，另一些则需要您短短两个粉。 请参阅贵国制造商的文件。 这可以根据您正在使用的设备来实现。 有些SBC有一个按钮，另一些则需要您短短两个粉。 请参阅贵国制造商的文件。 这可以根据您正在使用的设备来实现。 有些SBC有一个按钮，另一些则需要您短短两个粉。 请参阅贵国制造商的文件。

- 通过谷歌搜索可以轻松地找到此信息：

```
遮罩模式 <your sbcs name here>
```

- 为了验证您的设备是否处于`maskrom mode`并且您的 PC 运行正确地发现了：

```
sudo rkdeveloped toold
```

- 如果你看到以下情况，你很好了 (输出相似，但不是相同):

```
DevNo=1 Vid=0x2207, Pid=0x350b,LocationID=801 Maskrom
```

## 3.2 FlashBredOS

现在我们能够使用 "rkdeveloped tool" 发送命令到设备中，让我们使用 BredOS SBC 来制作。

- 向 SBC 发送SPI 加载文件：

```
sudo rkdeveloped tools db <path to SPI loader file here>
```

- 然后将 BredOS 设备特定图像写入到 eMMC 中：

```
sudo rkdeveloped tools wl 0 <path to BredOS image here>
```

- 最后重启您的设备：

```
sudo rkdevelopmenttoold
```

> 在刷入成功后，继续进行 [**First Setup**](/en/install/first-setup)。
> {.is-success}
> {.is-success}
> {.is-success}