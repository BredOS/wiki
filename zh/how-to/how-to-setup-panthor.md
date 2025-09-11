---
title: :paw_prints：如何在马里使用 RK3588 设置Panthor GPU
description:
published: true
date: 2025-09-11T18：23：22.464Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 使用 RK3588 :routha 在马里启用Panthor GPU

这个指南使你走过让马里的 Panthor 和 Vulkan 在 RK3588 芯片的板上有 GPU 的步骤。

# 🔧 启用Panthor的步骤

### 🎛️ 1. 启用Panthor DTBO

按照[设备树叠加层指南](/how-to/how-to-enable-dtbos)启用
`/boot/dtbs/rockchip/overy/rockchip-rk3588-panthor-gpu.dtbo`
**复制DTBO后，不要重启系统！**

### 🔄 2. 替换面板图形

用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

### 🌋 3. 启用 Vulkan

安装vulkan加载器和驱动器：

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

### 🔁 4. 重启您的系统

如果您想要验证您的图形，您可以运行以下操作：

```
sudo pacman -S inxi mesa-utils
inxi -G
```