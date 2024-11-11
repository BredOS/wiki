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

## Important directories
Inside the `sbc-pkgbuilds` repository there is a folder named `linux-rockchip-rkr3`.
It should be used as the current working directory during building.
