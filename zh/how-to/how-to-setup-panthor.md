---
title: 如何在马里安装Panthor GPU with RK3588
description:
published: true
date: 2026-01-20T10:04:59.437Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 🎛️ 1. 简介

这个指南使你走过让马里的Panthor GPU 存在于RK3588 chipset的板上。

## 1.1 Panthor和Panfork之间的差别是什么？

Panthor 是马里G\*\*\* gpus开发者开发的 linux 内核的一个新驱动程序。 潘福克是邦弗斯特的一个分叉，其目的是支持马里610集团获释后的工作。 即使如此，邦福克比潘索表现更好，潘托尔也是继续支持邦福克的道路。

- Panthor的性能概述：

```
> EGL (2D acceleration) performance ~-40% (not measured, answering from day to day feel).
> OpenGL (3D acceleration) performance -16%.
> Vulkan is now almost fully supported.
> You also see a bit more cpu usage (~5%) on heavy gpu usage.
```

> RK35xx 设备的 BredOS 默认启用了Panfork ！
> {.is-info}

# 🔄 2. Install Panthor

## 2.1 Enable the DTBO

### 2.1.1 Automatically

- bredos-config 工具提供了一种简单的方式来启用和禁用 dtbos。 启动工具为 启动工具： 启动工具： 启动工具： 启动工具： 启动工具：

```
sudo bredos-config
```

然后导航到`设备树管理器` -> `启用/禁用叠加层` 并启用 `rockchip-rk3588-panthor-gpu` 。 该工具然后安装基础设备树和所选叠加层。 该工具然后安装基础设备树和所选叠加层。 该工具然后安装基础设备树和所选叠加层。

> Do not reboot your system after the installation of the dtb overlay!
> {.is-warning}

bredos-config 能够安装 dtbs 并更改grub 配置以便在启动时加载它_不能_ 更改uefi 设置。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。

> 不要在安装dtb 覆盖后重启系统！
> {.is-warning}
> {.is-warning}
> Continue with `2.2 Replace Panfork graphics`.
> {.is-warning}

### 2.1.2 Manually

Follow the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos) to enable `/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`.

> Do not reboot your system after the installation of the dtb overlay!
> Continue with `2.2 Replace Panfork graphics`.
> {.is-warning}

## 2.2 Replace Panfork graphics

- 用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

## 2.3 Enable Vulkan

- 安装vulkan加载器和驱动器：

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

## 2.4 Reboot Your System

- 重启系统以应用更改。

## 2.5 Validate Installation

- 如果您想要验证您的图形，您可以运行以下操作：

```
lsmod | grep pan
```

The output of the command above should indicate that the `panthor` module is loaded. If you still see the `panfrost` module listed, you may want to check if you have done all steps described in this article.

# 🔁 3. Revert to Panfrost

- To revert to `Panfork`, run the following commands:

### Tabset {.tabset}

#### UEFI-based System

```
sudo pacman -S mesa-panfork-git
rm /boot/efi/dtb/overlays/rockchip-rk3588-panthor-gpu.dtbo
sudo reboot
```

#### U-Boot-based System

```
sudo pacman -S mesa-panfork-git
sudo nano /boot/extlinux/extlinux.conf
```

Remove the line `fdtoverlays /boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`.
Then Save and Close.

- Reboot your system to apply your changes:

```
sudo reboot
```

