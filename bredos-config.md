---
title: BredOS Config
description: 
published: true
date: 2025-09-23T10:12:11.659Z
tags: 
editor: markdown
dateCreated: 2025-09-21T09:27:04.136Z
---

# 1. Introduction
- The `bredos-config` tool has been developed to simplify system changes, maintenance, and management for you.

![main.png](/bredos-config/main.png)

> The tool `bredos-config` is installed by default. 
{.is-info}

- If you removed it and/or want to reinstall it, run:
```
sudo pacman -S bredos-config
```

# 2. Features
## 2.1 Device Tree Manager
- This option helps you manage device trees and device tree overlays, which are used to alter how the kernel interacts with your device. A simple example would be using them to disable the LED on an Orange Pi 5 Plus, but there is much more to explore. Follow [this article](/how-to/how-to-enable-dtbos) to learn more about it.

![dtb-manager.png](/bredos-config/dtb-manager.png)

## 2.2 Update the system

> This option is currently under construction!
{.is-warning}

![update.png](/bredos-config/update.png)

## 2.3 System Upkeep
- In this section, you'll find some useful tasks to keep your system clean and running smoothly like Performing Filesystem Maintenance tasks or checking you system integrity.

![upkeep.png](/bredos-config/upkeep.png)

## 2.4 System Tweaks
- Here you can find some useful tweaks to your system:

![tweaks.png](/bredos-config/tweaks.png)

## 2.5 Migrations

> This option is currently under construction!
{.is-warning}

![migrations.png](/bredos-config/migrations.png)

## 2.6 Packages
- Here, you'll find various hooks to help you install cool things, like steam or docker, properly:

![packages.png](/bredos-config/packages.png)