---
title: 📟 如何启用 DTBOs
description:
published: true
date: 2025-05-15T13:00:37.165Z
tags:
editor: markdown
dateCreated: 2024-11-10T18：02：07.427Z
---

# 如何启用设备树覆盖

**Introduction**
启用不同的设备树叠加层(DTBOs) 允许启用可选的硬件或内核修改，而无需重新编译Linux内核。
这也是开启地形图堆栈的预定方式。
这也是开启地形图堆栈的预定方式。

---

# 💻 For UEFI-power Systems

如果您在UEFI驱动的板上运行，您需要配置它。
如果你已经这样做了，你可以先跳过步骤5。
如果你已经这样做了，你可以先跳过步骤5。

> 2024年9月12日之后的图像使用`/boot/efi`而不是`/boot`。
> {.is-info}
> {.is-info}

要确定您的 ESP 分区所在位置，请运行命令。
`df | grep "/boot" | awk '{print $NF}'，**替换** <ESP>` **以下所有命令**以输出替换。

### 📁 1: 创建存储DTB 文件的必要目录

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

### 🗄️ 2: 复制到基础DTB

> 如果您正在使用 FydeTab Duo, 请将指定的DTB 文件复制到 `base` 文件夹：
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tab-12c-linux.dtb
> ```

{.is-info}

对于其他基于 RK3588的看板，用您的实际设备名称替换 \\\\\`rk3588-board.dtb' ：

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

### 🫘 3: 配置 GRUB

打开 GRUB 配置文件：

```
sudo nano /etc/default/grub
```

在开头添加一个 "#" 来评论下面的行：

```
# GRUB_DTB="dtbs/rockchip/device-tree.dtb"
```

_(您的DTB将与此不同)_

更新GRUB的新配置：

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🎛️ 4: 配置 UEFI

重启到 UEFI _(您可以从 GRUB做到这一点)_ > `设备管理器` > `Rockchip 平台配置` > `ACPI / 设备树` ，并做以下操作：

- **将“配置表模式”设置为“设备树”**
- **更改为 `Enabled`** 支持 DTB 覆盖和叠加层\\\\\`

![](/panthor/enable_tree_dtb_in_uefi.jpg)

按 F10 可保存并重新启动到您的系统 (您可以返回到第一个UEFI 屏幕并选择 `Continue`)。

### 🔄 5: 复制 DTBO

用“dtbo”代替`my-overlay`。

```
sudo cp /boot/dtbs/rockchip/overy/my-overlay.dtbo <ESP>/dtb/overy/
```

### 二维码: 重启

重新启动您的系统以应用更改。

# ⚙️ On U-Boot Powered Devices

### 1. 编辑 extlinux 配置

运行 extlinux 配置可以编辑：

```
sudo nano /boot/extlinux/extlinux.conf
```

将以下行添加到文件底部，用您选择的一个取代DTBO：

```
fdtovery/dtbs/rockchip/overy/my-overlay.dtbo
```

### 未输入

**DO NOT** 在这些行中添加`/boot`或`<ESP>`物品。

**不要** 添加多个“fdtovery”行。
**不要** 添加多个“fdtovery”行。
如果您想要启用多个DTBO，请将其附在一条直线上，由空白处隔开。
例如：
例如：

```
fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
```