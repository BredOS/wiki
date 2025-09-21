---
title: Run Android apps (waydroid)
description: 
published: false
date: 2025-09-21T08:40:19.752Z
tags: 
editor: markdown
dateCreated: 2025-09-21T08:40:19.752Z
---

# Introduction

# 1. Installation

Install Waydroid
```
sudo pacman -S waydroid waydroid-image-panthor
```

Initialize waydroid:

[`sudo waydroid init -s GAPPS`]: # 

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

Enable and start Waydroid
```
sudo systemctl enable --now waydroid-container
```

# 2. Install apps
Download apk and run:
```
waydroid app install <apk>.apk
```