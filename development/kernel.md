---
title: Kernel modding
description: 
published: true
date: 2024-11-11T12:14:07.650Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# Kernel modding
This guide primarily focuses on RK3588 and the linux-rockchip-rkr3 kernel.
This guide should however mostly carry over to other kernels.

## BredOS kernel Repository
BredOS stores it's linux-rockchip kernel fork at:
https://github.com/BredOS/linux-rockchip

The branch used for the rkr3 kernel is `rk6.1-rkr3`.
The mainline variant is instead at `rk-mainline`.

## BredOS kernel PKGBUILD
THe kernel is built and packages with the PKGBUILDs from:
https://github.com/BredOS/sbc-pkgbuilds

## Building the kernel
Under ARM systems, just : 
```bash
make -j4
```

Under x86 systems, we need to cross-compile the kernel:
```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j4
```

You should see the image in the `arch/arm64/boot/` directory.

## Important directories
Inside the `sbc-pkgbuilds` repository there is a folder named `linux-rockchip-rkr3`.
It should be used as the current working directory during building.
