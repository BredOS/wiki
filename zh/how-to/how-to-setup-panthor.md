---
title: 安装在马里的Panthor GPU with RK3588
description:
published: true
date: 2025-09-18T07:07:37.654Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 1. 简介

这个指南使你走过让马里的Panthor GPU 存在于RK3588 chipset的板上。

# 2. 启用Panthor DTBO

## 2.1 自动使用

- bredos-config 工具提供了一种简单的方式来启用和禁用 dtbos。 启动工具为 启动工具：

```
sudo bredos-config
```

然后导航到`设备树管理器` -> `启用/禁用叠加层` 并启用 `rockchip-rk3588-panthor-gpu` 。 该工具然后安装基础设备树和所选叠加层。

> 仔细遵循屏幕上的说明！
> {.is-warning}
> {.is-warning}

bredos-config 能够安装 dtbs 并更改grub 配置以便在启动时加载它_不能_ 更改uefi 设置。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。 此操作必须由用户完成。 用户必须做出的更改通过基本/叠加层数据库首次安装时的面包配置来显示。 更改也可以在 [设备树叠加层指南](/how-to/how-to-enable-dtbos) 中找到。

> 不要在安装dtb 覆盖后重启系统！
> {.is-warning}
> 继续使用 \`3。 替换Panfork 图形。
> {.is-warning}

## 2.2 手动操作

按照[设备树叠加层指南](/how-to/how-to-enable-dtbos)启用
`/boot/dtbs/rockchip/overy/rockchip-rk3588-panthor-gpu.dtbo`
**复制DTBO后，不要重启系统！**

> 不要在安装dtb 覆盖后重启系统！
> {.is-warning}
> 继续使用 \`3。 替换Panfork 图形。
> {.is-warning}

# 3. 替换面板图形

- 用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

# 4. 重启您的系统

- 安装vulkan加载器和驱动器：

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

# 5. 重启您的系统

- 重启系统以应用更改。 如果您想要验证您的图形，您可以运行以下操作：

```
sudo pacman -S inxi mesa-utils
inxi -G
```