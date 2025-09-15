---
title: How to install STEAM on BredOS
description: A simple guide to install Steam on BredOS, with step-by-step instructions for both Panthor-enabled and non-Panthor configurations.
published: true
date: 2025-09-15T09:14:13.344Z
tags: 
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 1. Introduction

Welcome to the guide on how to install **Steam** on BredOS! Follow these simple steps to get Steam up and running on your system.

## 2. Prerequisites
> This how-to is meant for Rockchip RK35xx devices!
{.is-info}

- You need to have **BredOS** installed and running.
- Optionally, you can have [Panthor enabled](/how-to/how-to-setup-panthor), but it's not required.

## 3. Installation Steps
### 3.1 Automatically

- The tool `bredos-config` offers a simple way to install steam and the appropriate steam-libs. Start the tool with
```
sudo bredos-config
```
- Then navigate to `Packages` -> `Install Steam`. Steam will then be installed. Easy, right?

### 3.2 Manually
#### 3.2.1 In case of using an older BredOS image:

You may need to add the **BredOS Multilib** repository to install Steam and the necessary translation layers. To do this, follow these steps:

- Install `bredos-multilib` package
```
   sudo pacman -S bredos-multilib
```

- Update the package database by running:

```
   sudo pacman -Sy
```

#### 3.2.2 Steam Installation:


- Run the following command to install Steam:

```
   sudo pacman -S steam
```

- After executing the command, you will see a message prompting you to select an option. Choose the appropriate option based on your configuration:

- First, select `lib32-vulkan-swrast`

![steam_libs_selection.png](/steam_libs_selection.png)

- If you have **Panthor** enabled, select `steam-libs-any`.
- If **Panthor** is not enabled (using Panfork instead), select `steam-libs-rk3588`.

- Wait for the installation to complete and you're all set.

## 4. Uninstalling Steam

- If you need to uninstall Steam and reset the configuration to choose a different option:

```
sudo pacman -Rnscu steam steam-libs-any #or steam-libs-rk3588 depending on your selection
```

## 5. Launch Steam

- Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:

```
steam
```

> Happy gaming!
{.is-success}

