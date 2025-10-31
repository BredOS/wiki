---
title: 运行 Android 应用程序(waydroid)
description:
published: true
date: 2025-09-26T10:03:46.309Z
tags:
editor: markdown
dateCreated: 2025-09-21T08：40：19.752Z
---

# 1. 简介

Waydroid 是基于 Wayland 在 Linux / GNU 上运行 Android 的一个基于容器的解决方案。 本指南将带你走上安装它的必要步骤。 本指南将带你走上安装它的必要步骤。 本指南将带你走上安装它的必要步骤。 本指南将带你走上安装它的必要步骤。 本指南将带你走上安装它的必要步骤。

# 2. 安装

- Install Waydroid:

```
sudo pacman -S waydroid
```

## 2.1 RK3588

您需要启用全景并进行设置。 要做到这一点，请关注[本指南](/how-to/how-to-setup-panthor)。

- Install panthor image:

```
sudo pacman -S waydroid-panthor-image
```

- Initialize waydroid:

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

## 2.2 通用ARM64/X86_64

- 这将下载并安装 GAPPS 版本的 android:

```
sudo waydroid init -s GAPPS
```

# 3. 启用并启动 waydroid

- 启用并启动 Waydroid:

```
sudo systemctl 启用 --now waydroid-container
```

- 然后启动您的货运机器人容器：

```
waydroid 会话开始
```

# 4. 安装应用

- 下载apk 并运行：

```
安装 <apk>.apk
```

# 4. 安装应用

默认情况下，Waydroid总是以全屏方式运行。

- 如果您想要连接到桌面环境窗口管理器，请运行：

```
waydroid prop 设置持续.waydroid.multi_window true
```

然后重启您的航行会话。