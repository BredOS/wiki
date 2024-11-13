---
title: 内核moding
description: null
published: true
date: 2024-11T12：14：07.650Z
tags: null
editor: markdown
dateCreated: 2024-11T11:49:44.206Z
---

# 内核moding

本指南主要侧重于RK3588 和 linux-rockchip-rkr3 内核。
但本指南大多应传送到其他内核。

## BredOS 内核仓库

BredOS 存储它的 linux-rockchip 内核fork 于:
https://github.com/BredOS/linux-rockchip

用于rkr3内核的分支是 `rk6.1-rkr3` 。
主线变量转为“rk-mainline”。

## BredOS kernel PKGBUILD

他的内核是用PKGBUILD构建的：
https://github.com/BredOS/sbc-pkgbuild来构建和软件包

## 重要目录

在 `sbc-pkgbuilds` 里有一个名为`linux-rockchip-rkr3`的文件夹。
在构建过程中，它应作为当前的工作目录。
