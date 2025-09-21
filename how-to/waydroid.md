---
title: Run Android apps (waydroid)
description: 
published: false
date: 2025-09-21T08:43:39.064Z
tags: 
editor: markdown
dateCreated: 2025-09-21T08:40:19.752Z
---

# Introduction

# 1. Installation

Install Waydroid
```
sudo pacman -S waydroid
```

## 1.1 RK3588

You need panthor enabled and setup follow this guide [how-to-setup-panthor](/how-to/how-to-setup-panthor)
Install panthor image

```
sudo pacman -S waydroid-panthor-image
```

Initialize waydroid:

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

## 1.2 Generic ARM64/X86_64

This will download and install the GAPPS version of android:
```
sudo waydroid init -s GAPPS
```

# 2. Enable and start waydroid

Enable and start Waydroid
```
sudo systemctl enable --now waydroid-container
```

# 3. Install apps
Download apk and run:
```
waydroid app install <apk>.apk
```