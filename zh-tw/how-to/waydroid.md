---
title: Run Android apps (waydroid)
description:
published: false
date: 2025-09-21T08:56:04.025Z
tags:
editor: markdown
dateCreated: 2025-09-21T08:40:19.752Z
---

# 1. 簡介

Waydroid is a container-based solution for running Android on Linux/GNU using Wayland. This guide will walk you through the necessary steps to install it.

# 2. 安裝

- Install Waydroid:

```
sudo pacman -S waydroid
```

## 2.1 RK3588

You need panthor enabled and setup follow [this guide](/how-to/how-to-setup-panthor).

- Install panthor image:

```
sudo pacman -S waydroid-panthor-image
```

- Initialize waydroid:

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

## 2.2 Generic ARM64/X86_64

- This will download and install the GAPPS version of android:

```
sudo waydroid init -s GAPPS
```

# 3. Enable and start waydroid

- Enable and start Waydroid:

```
sudo systemctl enable --now waydroid-container
```

# 4. Install apps

- Download apk and run:

```
waydroid app install <apk>.apk
```