---
title: Fydetab上的 GNOME
description: null
published: true
date: 2024-11T10：39：09.164Z
tags: null
editor: markdown
dateCreated: 2024-11-10T19：41：06.111Z
---

# FydetabDuo 上的 GNOME 桌面

gnome-desktop 可以与软件包`gnome-meta`安装。

---

为了正常操作，您也应该在安装时切换到GDM。 要做到这一点，就必须：

```
sudo systemctl 禁用 lightdm
sudo systemctl 启用 gdm
```

只支持Gnome路地。

## 屏幕旋转修复

**如果** 你的 Fydetab 屏幕旋转不正确，你需要安装和配置 `Screen Rotate` 扩展。

### 1. 安装扩展管理器

运行 `sudo pacman -S extension-manager` 来安装它，并打开应用程序。

### 2. 安装屏幕旋转

打开应用后，点击 `Browse` > `Search` > 输入 `Screen rotate` > 安装 `Screen Rotate` by `shyzus` 。

### 3. 配置屏幕旋转

返回扩展管理器的 "已安装" 页面并点击设置认知器打开扩展的设置面板。
然后你应该将 "设置方向偏移" 的值增加到1。

## 横向风格使用量

样式只有当屏幕默认垂直旋转时才会正确点数。
若要将此设置为水平工作，请使用：

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

### 3. Reboot

重启后笔会正常工作。

如果您错误地尝试忽略设置的样式表校准，请通过运行以下操作移除校准数据：

```
dconf 重置 -f /org/gnome/desktop/外围/平板电脑
```
