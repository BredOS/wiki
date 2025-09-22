---
title: 内核moding
description:
published: true
date: 2025-09-17T09:55:53.063Z
tags:
editor: markdown
dateCreated: 2024-11T11:49:44.206Z
---

# 1. 简介

本指南主要侧重于RK3588和`linux-rockchip-rkr3`内核。
但本指南大多应传送到其他内核。
但本指南大多应传送到其他内核。

# 2. 获取内核或其源代码

## 2.1 BredOS 内核仓库

BredOS stores it's `linux-rockchip` kernel fork at:
https://github.com/BredOS/linux-bredos

用于rkr3内核的分支是 `rk6.1-rkr3` 。
主线变量转为“rk-mainline”。
主线变量转为“rk-mainline”。

## 2.2 BredOS kernel PKGBUILD

内核是用PKGBUILD构建的：
https://github.com/BredOS/sbc-pkgbuild来构建和软件包

## 2.3 建造内核

- 在ARM系统下，只需使用：

```bash
make -j$(nproc)
```

- 在 x86 系统下，我们需要交叉编译内核：

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

你应该在 `arch/arm64/boot/` 目录中找到内核图像。

> 在 `sbc-pkgbuilds` 里有一个名为`linux-rockchip-rkr3`的文件夹。
> 在构建过程中，它应作为当前的工作目录。
> 在构建过程中，它应作为当前的工作目录。
> {.is-info}

# 3. 编译设备树和叠加

使用`dtsc`、BredOS工具编译DTB和DTBO的完整指南现已可供使用。
点击 [here]/Tools#dtsc-helper-script) 查看它。
Click [here](/Tools#dtsc-helper-script) to view it.