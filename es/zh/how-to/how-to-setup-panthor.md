---
title: :paw_prints：如何在马里使用 RK3588 设置Panthor GPU
description: null
published: true
date: 2024-09-01T16：18：22.222Z
tags: null
editor: markdown
dateCreated: 2024-31T15:03:26.994Z
---

# 使用 RK3588 :routha 在马里启用Panthor GPU

这个指南使你走过让马里的Panthor GPU 存在于RK3588 chipset的板上。

# 🔧 启用Panthor的步骤

## 在 UEFI 启用的设备

### 🖥️ 1. 在 UEFI 上初始设置

首先,为 DTB 文件创建必要的目录：

```
sudo mkdir -p /boot/dtb/{base,overlays}
```

接下来,配置您的 UEFI 设置。 启动到 UEFI > 设备管理器 > Rockchip 平台配置 > ACPI / 设备树,执行以下操作：

- **将“配置表模式”设置为“设备树”**
- **更改为 `Enabled`** 支持 DTB 覆盖和叠加层\\`

![](/panthor/enable_tree_dtb_in_uefi.jpg)

按F10键保存并启动到您的系统 (您可以返回到第一个UEFI屏幕并选择 `Continue`)。

### 🛠️ 3. 设置设备树

> 如果您正在使用 FydeTab Duo, 请将指定的DTB 文件复制到 `base` 文件夹：
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb /boot/dtb/base/
> sudo cp /boot/dtb/base/rk3588s-fydetab-duo.dtb /boot/dtb/base/rk3588s-tablet-12c-linux.dtb
> ```

{.is-info}

► ： RK3588

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb /boot/dtb/base/
```

### 🌐 4. 所有看板的常用设置

不管您在使用什么板,复制DTBO叠加层文件以启用 Panthor：

```
sudo cp /boot/dtbs/rockchip/overy/rockchip-rk3588-panthor-gpu.dtbo /boot/dtb/overy/
```

此外,您需要修改 GRUB 配置：

打开 GRUB 配置文件

```
sudo nano /default/grub
```

在开头添加一个 "#" 来评论下面的行：

```
# GRUB_DTB="dtbs/rockchip/rk3588s-fydetab-duo.dtb"
```

使用新的配置更新 GRUB

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🔄 5. Meta panfork-git

用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

### 🔁 6. 重启您的系统

## ⚙️ U-启动设备启用

### 1. 启用Panthor DTBO

编辑要应用叠加层的 `extlinux` 配置文件：

```
sudo nano /boot/extlinux/extlinux.conf
```

在 `extlinux.conf` 文件中添加以下一行：

```
fdtoverlays /dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo
```

### 🔄 2. Meta panfork-git

用标准的`mesa`软件包替换`mesa-panfork-git`软件包：

```
sudo pacman -S mesa
```

### 🔁 3. 重启您的系统
