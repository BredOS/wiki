---
title: Kernel modding
description: 
published: false
date: 2025-11-03T08:51:43.991Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# 1. Introduction

This guide primarily focuses on RK3588 and the linux-rockchip-rkr3 kernel; however, the general process and many of the concepts should also apply to other Rockchip-based kernels and devices. Whether you are developing custom firmware, contributing to upstream kernel support, or simply seeking to understand how the Linux kernel is built for ARM64 hardware, this article aims to provide a clear and practical starting point.

# 2. Obtaining the kernel or it's source code
## 2.1 BredOS kernel Repository

BredOS stores it's `linux-rockchip` kernel fork at [https://github.com/BredOS/linux-bredos](https://github.com/BredOS/linux-bredos).

The branch used for the rkr3 kernel is `rk6.1-rkr3`, the mainline variant is instead at `rk-mainline`. While rkr3 (aka Legacy (stable) aka BSP) is the kernel we ship with our "device specific images", mainline is the most up-to-date kernel which still has bugs and missing features.

> For more info have a look [here](/en/img-types).
{.is-info}


## 2.2 Building BredOS kernel with PKGBUILD
Like any custom PKGBUILD for BredOS, the kernel PKGBUILD can also be found at [https://github.com/BredOS/sbc-pkgbuilds](https://github.com/BredOS/sbc-pkgbuilds). 
- Clone the repository with:
```
git clone https://github.com/BredOS/sbc-pkgbuilds
```

This creates a folder with the name `sbc-pkgbuilds` in your current directory, which holds any custom package from our repository, including the kernel PKGBUILD.

- Change directory to the kernel PKGBUILD with:
```
cd sbc-pkgbuilds
cd linux-rockchip-rkr3
```

- The contents of that folder should be as follows:
```
PKGBUILD
bredos-update-dtbs
config
dtb-update.hook
linux.preset
```

- To compile and packages the kernel, run:
```
makepkg -si
```

> While the parameter `-s` automatically installs all necessary dependencies, the parameter `-i` installs the package after successful compiling.
{.is-info}


## 2.3 Building the kernel without PKGBUILD
It is also possible to build the kernel without using a PKGBUILD. This can be helpful if you wish to compile on a non-Arch-based Linux distribution, on Windows with WSL, or if you want to compile for a different CPU architecture.

- Install all necessary dependencies on your system. For Arch-based distribution the command is:
```
sudo pacman -Syu base-devel
```

- If you want to cross-compile a aarch64 kernel on a x86_64 system install:
```
sudo pacman -S aarch64-linux-gnu-gcc
```

- Then clone our kernel repository with:
```
git clone -b rk6.1-rkr3 https://github.com/BredOS/linux-bredos
```

> If you want to build a different branch, such as `rk-mainline`, set the `-b` parameter accordingly.
{.is-info}

- Change directory with:
```
cd linux-bredos
```

- If your compilation system is already based on the target CPU architecture, simply use: 
```bash
make -j$(nproc)
```

- If not, we need to cross-compile the kernel with (for building a aarch64 kernel):
```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

You should find the kernel image in the `arch/arm64/boot/` directory.

> Inside the `sbc-pkgbuilds` repository there is a folder named `linux-rockchip-rkr3`.
> It should be used as the current working directory during building.
{.is-info}


# 3. Compiling Device Trees and Overlays

A complete guide for using `dtsc`, the BredOS tool for compiling DTB and DTBOs is now available. Click [here](/Tools#dtsc-helper-script) to view it.