---
title: 如何启用 DTBOs
description:
published: true
date: 2025-09-16T10:44:14.092Z
tags:
editor: markdown
dateCreated: 2024-11-10T18：02：07.427Z
---

# 1. 编辑 extlinux 配置

启用不同的设备树叠加层(DTBOs) 允许启用可选的硬件或内核修改，而无需重新编译Linux内核。

> 这也是改变内核行为的预定方式。 例如，启用全景图堆栈或禁用您系统上的引导。
> {.is-success}

# 2. BredOS-配置

- bredos-config 工具提供了一种简单的方式来启用和禁用 dtbos。 启动工具为 启动工具为 启动工具为

```
sudo bredos-config
```

然后导航到`设备树管理器` -> `启用/禁用叠加层` 并启用 dtb 叠加层以满足您的需要。 工具然后安装基础设备树和选定的叠加层。 重启系统以应用更改。 工具然后安装基础设备树和选定的叠加层。 重启系统以应用更改。

bredos-config 可以安装 dtbs 并更改grub 配置以便在启动时加载它们。_不能_更改UEFI设置。 此操作必须由用户完成。 用户必须做出的更改，可以在首次安装基础/叠加层dbs时通过面包配置或者使用 “3.4 配置 EFI” 显示。 如果您的设备是 u-boot-based，则不需要进一步更改。 此操作必须由用户完成。 用户必须做出的更改，可以在首次安装基础/叠加层dbs时通过面包配置或者使用 “3.4 配置 EFI” 显示。 如果您的设备是 u-boot-based，则不需要进一步更改。

> 如果你在棋盘上看到一个 BredOS 标志，你正在使用 UEFI 。
> {.is-warning}
> {.is-warning}

> 这是建议启用/禁用 dtb 叠加层的方式。 如果您使用 `bredos-config` ，下面的步骤将不会有花蜜。
> {.is-success}

# 3. 为UEFI供电系统

如果您在UEFI驱动的板上运行，您需要配置它。
如果你已经这样做了，你可以先跳过步骤5。
如果你已经这样做了，你可以先跳过步骤5。

> 2024年9月12日之后的图像使用`/boot/efi`而不是`/boot`。
> {.is-info}
> {.is-info}

要确定您的 ESP 分区所在位置，请运行命令。
`df | grep "/boot" | awk '{print $NF}'，**替换** <ESP>` **以下所有命令**以输出替换。

## 3.1 创建存储DTB文件的必要目录

- _(您的DTB将与此不同)_

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

## 🗄️ 2: 复制到基础DTB

> 如果您正在使用 FydeTab Duo, 请将指定的DTB 文件复制到 `base` 文件夹：
>
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tab-12c-linux.dtb

- 对于其他基于 RK3588的看板，用您的实际设备名称替换 \\\\\`rk3588-board.dtb' ：

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

## 🫘 3: 配置 GRUB

- 打开 GRUB 配置文件：

```
sudo nano /etc/default/grub
```

- 在开头添加一个 "#" 来评论下面的行：

```
# GRUB_DTB="dtbs/rockchip/device-tree.dtb"
```

- 更新GRUB的新配置：

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 🎛️ 4: 配置 UEFI

- 按 F10 可保存并重新启动到您的系统 (您可以返回到第一个UEFI 屏幕并选择 `Continue`)。

> 如果您需要帮助，则有一个 [guide](/en/how-to/change-default-boot-order-rk3588) 来更改启动顺序。 在其最初的步骤中，它会显示您如何启动到 UEFI 设置。
> {.is-info} 在其最初的步骤中，它会显示您如何启动到 UEFI 设置。
> {.is-info}

- 浏览至`设备管理器` > `Rockchip 平台配置` > `ACPI / 设备树`

- **将“配置表模式”设置为“设备树”**

- **更改为 `Enabled`** 支持 DTB 覆盖和叠加层\\\\\\`

![](/panthor/enable_tree_dtb_in_uefi.jpg)

- 按 F10 键保存并重新启动到您的系统。

## 🔄 5: 复制 DTBO

- 使用 dtbo 替换<my-overlay>\\`。

```
sudo cp /boot/dtbs/rockchip/overy/my-overlay.dtbo <ESP>/dtb/overy/
```

## 3.6 Reboot

- 重新启动您的系统以应用更改。

# 4. U-启动药水设备

## 4.1 编辑 extlinux 配置

- 运行 extlinux 配置可以编辑：

```
sudo nano /boot/extlinux/extlinux.conf
```

- 将以下行添加到文件底部，用您选择的一个取代DTBO：

```
fdtovery/dtbs/rockchip/overy/my-overlay.dtbo
```

> **不要** 添加多个“fdtovery”行。
> **不要** 添加多个“fdtovery”行。
> 如果您想要启用多个DTBO，请将其附在一条直线上，由空白处隔开。
> 例如：
> 例如：
>
> fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
