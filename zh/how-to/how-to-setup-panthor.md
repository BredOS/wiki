---
title: :paw_prints：如何在马里使用 RK3588 设置Panthor GPU
description: null
published: true
date: 2024-11-10T19：29：32.381Z
tags: null
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 使用 RK3588 :routha 在马里启用Panthor GPU

这个指南使你走过让马里的Panthor GPU 存在于RK3588 chipset的板上。

# 🔧 启用Panthor的步骤

### 🎛️ 1. 启用Panthor DTBO

Follow the [Device Tree Overlay guide](https://wiki.bredos.org/en/how-to/how-to-enable-dtbos) to enable
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**Do not reboot your system after copying the DTBO!**

### 🔄 2. 替换面板图形

用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

### 🔁 3. 重启您的系统

如果您想要验证您的图形，您可以运行以下操作：

```
sudo pacman -S inxi mesa-utils
inxi -G
```