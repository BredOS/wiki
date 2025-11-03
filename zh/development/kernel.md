---
title: 内核moding
description:
published: false
date: 2025-11-03T08:51:43.991Z
tags:
editor: markdown
dateCreated: 2024-11T11:49:44.206Z
---

# 4. 重要目录

本指南主要侧重于RK3588 和 linux-rockchip-rkr3 内核； 然而，一般进程和许多概念也应适用于其他基于 Rockchip的内核和装置。 您是否正在开发自定义固件，有助于上游内核支持。 或只是设法了解Linux内核是如何为ARM64硬件构建的，本条旨在提供一个明确和实际的出发点。

# 2. BredOS kernel PKGBUILD

## BredOS 内核仓库

BredOS 在 [https://github.com/BredOS/linux-bredos](https://github.com/BredOS/linux-bredos) 存储它的 `linux-rockchip` 内核叉。

用于rkr3内核的分支是 `rk6.1-rkr3`，主线变量则在 `rk-mainline` 处。 当rkr3(又名遗产(稳定)又名BSP)是我们用我们的“设备特定图像”运送的内核时， 主线是仍然有缺陷和缺失功能的最新内核。

> 更多信息有一个外观 [here](/en/img-types)。
> {.is-info}

## 2.2 使用 PKGBUILD 建造BredOS 内核

就像任何自定义的 BredOS PKGBUILD一样，内核也可以在 [https://github.com/BredOS/sbc-pkgbuilds](https://github.com/BredOS/sbc-pkgbuilds)找到。

- 复制资源库：

```
git clone https://github.com/BredOS/sbc-pkgbuilding
```

这将创建一个名为`sbc-pkgbuilds`的文件夹，在当前目录中保存我们仓库中的任何自定义包，包括内核PKGBUILD。

- 更改内核PKGBUILD目录：

```
cd sbc-pkgbuils
cd linux-rockchip-rkr3
```

- 该文件夹的内容应如下：

```
PKGBUILD
bredos-update-dtbs
config
dtb-update.hook
linux.preset
```

- 要编译和打包内核，请运行：

```
毫克-西文
```

> 虽然参数 `-s` 会自动安装所有必要的依赖关系，但参数 `-i` 会在编译成功后安装包。
> {.is-info}

## 2.3 不使用 PKGBUILD 构建内核。

不使用PKGBUILD也可以建造内核。 如果您想要编译非基于Archy的 Linux 发行版，这将是有用的。 在 WSL 窗口上，或者如果您想要编译不同的 CPU 架构。

- 安装所有必要的依赖于您的系统。 基于归档的分配命令是：

```
sudo pacman -Syu base-devel
```

- 如果您想要在一个x86_64 系统安装上交叉编译一个arch64内核：

```
sudo pacman -S aarch64-linux-gnu-gcc
```

- 然后克隆我们的内核仓库：

```
git clone -b rk6.1-rkr3 https://github.com/BredOS/linux-bredos
```

> 如果你想要构建一个不同的分支，例如`rk-mainline`, 相应设置`-b`参数。
> {.is-info}

- 更改目录：

```
cd linux-bredos
```

- 如果您的编译系统已经基于目标CPU结构，只需使用：

```bash
make -j$(nproc)
```

- 如果没有，我们需要用内核来交叉编译内核(用于构建无序64内核)：

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

您应该在 `arch/arm64/boot/` 目录中看到图像。

> 在 `sbc-pkgbuilds` 里有一个名为`linux-rockchip-rkr3`的文件夹。
> 在构建过程中，它应作为当前的工作目录。
> 在构建过程中，它应作为当前的工作目录。
> {.is-info}

# 3. 编译设备树和叠加

使用`dtsc`、BredOS工具编译DTB和DTBO的完整指南现已可供使用。
点击 [here]/Tools#dtsc-helper-script) 查看它。 Click [here](/Tools#dtsc-helper-script) to view it.