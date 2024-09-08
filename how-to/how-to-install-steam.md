---
title: How to install STEAM
description: A simple guide to install Steam on BredOS, with step-by-step instructions for both Panthor-enabled and non-Panthor configurations.
published: true
date: 2024-09-08T09:55:58.661Z
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
- Make sure you have **`pacman`** installed (this should already be available in BredOS).
- Optionally, you can have [**Panthor** enabled](https://wiki.bredos.org/en/how-to/how-to-setup-panthor), but it's not required.



## 📥 Installation Steps

1. Open your terminal 🖥️.
2. Run the following command to install Steam:
```
sudo pacman -S steam
```

3. After executing the command, you will see a message prompting you to select an option.

4. Choose the appropriate option based on your configuration:
   - If you have **Panthor** enabled, select **Option 3**.
   - If **Panthor** is not enabled, select **Option 5**.

5. Wait for the installation to complete and you're all set! 🎉

## 🚀 Launch Steam

Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:
```
steam
```
Happy gaming! 🎮✨
