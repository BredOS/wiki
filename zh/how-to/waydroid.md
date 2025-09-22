---
title: 运行 Android 应用程序(waydroid)
description:
published: true
date: 2025-09-21T12:54:43.353Z
tags:
editor: markdown
dateCreated: 2025-09-21T08：40：19.752Z
---

# 1. 简介

Waydroid 是基于 Wayland 在 Linux / GNU 上运行 Android 的一个基于容器的解决方案。 本指南将带你走上安装它的必要步骤。

# 2. 安装

- Install Waydroid:

```
sudo pacman -S waydroid
```

## 2.1 RK3588

您需要启用全景功能并关注[本指南](/how-to/how-to-setup-panthor)。

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

# 4. 安装应用

- 下载apk 并运行：

```
安装 <apk>.apk
```