---
title: 🎮 How to install STEAM on BredOS
description: A simple guide to install Steam on BredOS, with step-by-step instructions for both Panthor-enabled and non-Panthor configurations.
published: true
date: 2025-09-13T09:15:38.539Z
tags:
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 🎮 How to Install Steam on BredOS

Welcome to the guide on how to install **Steam** on BredOS! Follow these simple steps to get Steam up and running on your system.

## 🛠️ 1. Prerequisites

> This may not work on all devices (mainly non-RK3588 devices).
> {.is-info}

- You need to have **BredOS** installed and running.
- Optionally, you can have [**Panthor** enabled](/how-to/how-to-setup-panthor), but it's not required.

## 📥 2. Installation Steps

### 🤖 2.1 Automatically

The tool `bredos-config` offers a simple way to install steam and the appropriate steam-libs. Start the tool with

```
sudo bredos-config
```

and navigate to `Packages` -> `Install Steam`. Steam will then be installed. Easy, right?

### 🦶 2.2 Manually

#### 🔄 2.2.1 In case of using an older BredOS image:

You may need to add the **BredOS Multilib** repository to install Steam and the necessary translation layers. To do this, follow these steps:

- Install `bredos-multilib` package

```
   sudo pacman -S bredos-multilib
```

- Update the package database by running:

```
   sudo pacman -Sy
```

---

#### 🖥️ 2.2.2 Steam Installation:

- Run the following command to install Steam:

```
   sudo pacman -S steam
```

- After executing the command, you will see a message prompting you to select an option. Choose the appropriate option based on your configuration:

  - First, select `lib32-vulkan-swrast`

![steam\\_libs\\_selection.png](/steam_libs_selection.png)

- If you have **Panthor** enabled, select `steam-libs-any`.

- If **Panthor** is not enabled (using Panfork instead), select `steam-libs-rk3588`.

- Wait for the installation to complete and you're all set! 🎉

## 🔄 3. Uninstalling Steam

If you need to uninstall Steam and reset the configuration to choose a different option:

```
sudo pacman -Rnscu steam steam-libs-any #或 steam-libs-rk3588 視您的選擇而定
```

## 🚀 4. Launch Steam

Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:

```
steam
```

> **Happy gaming! 🎮✨**
> {.is-success}

