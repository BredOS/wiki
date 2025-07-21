---
title: Fydetab 上的 GNOME
description:
published: true
date: 2024-11-12T15:33:19.071Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:41:06.111Z
---

# FydetabDuo 上的 GNOME 桌面

GNOME 桌面可以在 AUR 包 `gnome-meta` 中安装。
使用 `yay -S gnome-meta` 安装它。

---

为了正常操作，您也应该在安装时切换到 GDM。要做到这一点，请运行：

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

只支持 Wayland 上的 GNOME。

## 屏幕旋转修复

**如果** 你的 Fydetab 屏幕旋转不正确，你需要安装和配置 `Screen Rotate` 扩展。

### 1. 安装扩展管理器

运行 `sudo pacman -S extension-manager` 来安装它，并打开应用程序。

### 2. 安装屏幕旋转

打开应用后，点击 `Browse` > `Search` > 输入 `Screen rotate` > 安装 `Screen Rotate` by `shyzus`。

### 3. 配置屏幕旋转

返回扩展管理器的 "已安装" 页面并点击设置图标打开扩展的设置面板。
然后你应该将 "设置方向偏移" 的值增加到 1。

## 横向触控笔使用

触控笔只有当屏幕默认垂直方向时才会正确工作。
要将此设置为水平工作，请使用：

### 1. 打开 `/etc/udev/rules.d/fydetab.rules`

要打开文件，请运行：

```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 2. 追加配置行

在文件底部添加：

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1 0 0 1"
```

然后按 Ctrl + S 键保存，Ctrl + X 键退出。

### 3. 重启

重启后触控笔会正常工作。

如果您错误地尝试忽略设置的触控笔校准，请通过运行以下操作移除校准数据：

```
dconf reset -f /org/gnome/desktop/peripherals/tablets
```