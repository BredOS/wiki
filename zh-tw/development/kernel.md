---
title: Kernel modding
description:
published: true
date: 2025-09-13T10:54:24.895Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# Kernel modding

This guide primarily focuses on RK3588 and the `linux-rockchip-rkr3` kernel.
This guide should however mostly carry over to other kernels.

## 1. BredOS kernel Repository

BredOS stores it's `linux-rockchip` kernel fork at:
https://github.com/BredOS/linux-bredos

The branch used for the rkr3 kernel is `rk6.1-rkr3`.
The mainline variant is instead at `rk-mainline`.

## 2. BredOS kernel PKGBUILD

The kernel is built and packages with the PKGBUILDs from:
https://github.com/BredOS/sbc-pkgbuilds

## 3. Building the kernel

Under ARM systems, just :

```bash
make -j$(nproc)
```

Under x86 systems, we need to cross-compile the kernel:

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

You should see the image in the `arch/arm64/boot/` directory.

## 4. Important directories

Inside the `sbc-pkgbuilds` repository there is a folder named `linux-rockchip-rkr3`.
It should be used as the current working directory during building.

## 5. Compiling Device Trees and Overlays

A complete guide for using `dtsc`, the BredOS tool for compiling DTB and DTBOs is now available.
Click [here](/Tools#dtsc-helper-script) to view it.