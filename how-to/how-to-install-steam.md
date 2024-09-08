---
title: How to install STEAM
description: A simple guide to install Steam on BredOS, with step-by-step instructions for both Panthor-enabled and non-Panthor configurations.
published: true
date: 2024-09-08T10:26:58.413Z
tags: 
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 🎮 How to Install Steam on BredOS

Welcome to the guide on how to install **Steam** on BredOS! Follow these simple steps to get Steam up and running on your system.

## 🛠️ Prerequisites
> Note: Steam seems to work only in X11 desktops
{.is-info}

- You need to have **BredOS** installed and running.
- Optionally, you can have [**Panthor** enabled](/en/how-to/how-to-setup-panthor), but it's not required.

## 📥 Installation Steps

### 🔄 In case of using an older BredOS image:

You may need to add the **BredOS Multilib** repository to install Steam and the necessary translation layers. To do this, follow these steps:

1. Install `bredos-multilib` package
```
   sudo pacman -S bredos-multilib
```

2. Update the package database by running:

```
   sudo pacman -Sy
```

---

### 🖥️ Steam Installation:

1. Open your terminal 🖥️.
2. Run the following command to install Steam:

```
   sudo pacman -S steam
```

3. After executing the command, you will see a message prompting you to select an option. Choose the appropriate option based on your configuration:
   - If you have **Panthor** enabled, select `steam-libs-any`.
   - If **Panthor** is not enabled (using Panfork instead), select `steam-libs-rk3588`.

4. Wait for the installation to complete and you're all set! 🎉

## 🔄 Uninstalling Steam

If you need to uninstall Steam and reset the configuration to choose a different option:

```
sudo pacman -Rnscu steam steam-libs-any #or steam-libs-rk3588 depending on your selection
```

## 🚀 Launch Steam

Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:

```
steam
```

**Happy gaming! 🎮✨**
