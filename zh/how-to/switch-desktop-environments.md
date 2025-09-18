---
title: 在 BredOS 上切换桌面环境
description: 学习如何在 BredOS 上安装并切换到 GNOME 桌面环境
published: true
date: 2025-09-18T07:46:58.501Z
tags: 自定义设置
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 1. BredOS 上的 GNOME 桌面

## 1.1 Install Gnome

GNOME 桌面环境可以与软件包`gnome`安装。\
要安装它，请运行：

- 要安装它，请运行：

```
pacman -S gnome
```

额外的 gnome-circle`可以安装额外的 gnome-circle`，它包含扩展GNOME 生态系统和 `gnome-extr` 等应用程序，其中包含开发工具以及一些非常适合GNOME的其他应用程序和游戏。

## 1.2 切换到GDM

要正常操作，您需要在安装后切换到 **GDM**。\
运行以下命令：

- 运行以下命令：

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

> 仅支持Wayland上的 GNOME。
> {.is-warning}
> {.is-warning}

## 1.3 屏幕旋转修复

**如果** 您的屏幕旋转不正确，您可以安装和配置**屏幕旋转** 扩展。

### 1.3.1 安装扩展管理器

- 运行：

```
sudo pacman -S extension-manager
```

安装完毕后，打开应用程序。

### 1.3.2 安装屏幕旋转

应用程序内：

- 点击 `Browse` > `Search`
- 键入“屏幕旋转”
- 通过 **shyzus** 安装 `Screen Rotate`。

### 1.3.3 配置屏幕旋转

- 转到扩展管理中的`已安装`选项卡。
- 点击装备图标打开扩展设置。
- 将"设置方向偏移"值增加到"1"。

## 1.4 风景风格使用

如果您的设备支持风格，它只会在屏幕默认垂直旋转时正确点数。
若要将此设置为水平工作，请按照这些步骤进行操作。

### 1.4.1 编辑udev规则

- 要编辑文件 `fydetab.rules`，请运行：

```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 1.4.2 追加配置行

- 在文件底部添加：

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1 0 0 1"
```

然后按 Ctrl + S 键保存，Ctrl + X 键退出。

# 2. BledOS 上的 Plasma 桌面

## 2.1 Install KDE Plasma

Plasma 桌面环境可以安装到软件包 "plasma-desktop"。\
要安装它，请运行：

- 要安装它，请运行：

```
pacman -S plasma-desktop
```

这将导致等离子体桌面安装最少。 这将导致等离子体桌面安装最少。 若要安装更完整的 KDE 体验，请选择软件包 `plasma` (它允许您选择您想要安装的Plasma相关软件包)，或选择`plasma-meta` 以获取全部内容。 Click [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) to understand the difference between a group and a meta package.
Click [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) to understand the difference between a group and a meta package.

> 避免使用 SDDM ，因为此软件已被遗弃！ 浅DM使用等离子体正常工作。
> {.is-warning} 浅DM使用等离子体正常工作。
> {.is-warning}
