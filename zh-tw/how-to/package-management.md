---
title: 📦✨ Package Managers Guide
description: Welcome to the BredOS Package Managers guide! 🚀 Here, you'll learn how to install and manage applications
published: true
date: 2024-09-20T20:10:47.203Z
tags:
editor: markdown
dateCreated: 2024-09-20T20:08:39.778Z
---

# 📦✨ Package Managers Guide

Welcome to the BredOS Package Managers guide! 🚀 Here, you'll learn how to install and manage applications. Get ready to take control of your system's apps! 💻

---

## 📚 Table of Contents

- Pacman 🐧
- Flatpak 📦
- AppImage 🖼️

---

## Pacman 🐧

**Pacman** 是 BredOS 的預設軟件包管理器，以其在管理軟件包時的速度和簡潔性而聞名。

### 如何安裝軟件包 🛠️

要使用 Pacman 安裝軟件包，請使用以下命令：

```bash
sudo pacman -S <package name>
```

### How to Update the System 🔄

To update all installed packages on your system, run:

```bash
sudo pacman -Syu
```

This will synchronize the package databases and upgrade all your packages to their latest versions.

### 如何移除軟件包 🗑️

要卸載軟件包，請使用：

```bash
sudo pacman -R <package name>
```

如果您想移除軟件包及其未使用的依賴項，請運行：

```bash
sudo pacman -Rns <package name>
```

### 如何搜索軟件包 🔍

要在 Pacman 儲存庫中搜索軟件包，請使用：

```bash
pacman -Ss <package name>
```

### Check Installed Packages 📋

To list all installed packages, simply run:

```bash
pacman -Q
```

### Clear Cache 🧹

To clear the Pacman cache and free up space, use:

```bash
sudo pacman -Sc
```

這將同步軟件包資料庫並將您所有的軟件包升級到最新版本。 ⚡🐧

---

## Flatpak 📦

**Flatpak** provides a sandboxed environment for running applications, independent of the host system’s software.

### How to Install Flatpak 🛠️

To install Flatpak, run:

```bash
sudo pacman -S flatpak
```

> **Note**: It may be necessary to reboot your system after installing Flatpak. 🔄

### How to Use Flatpak 📥

#### Install from Flathub 🌐

1. Navigate to [Flathub](https://flathub.org), find the app you want, and click install.
2. Copy the command in the terminal to complete the installation.

#### Install an App via Terminal ⌨️

You can also install apps directly from the terminal:

```bash
sudo flatpak install <app name>
```

#### Uninstall an App via Terminal 🗑️

To remove an app, run:

```bash
sudo flatpak uninstall <app name>
```

Alternatively, you can manage Flatpak apps using a graphical store like Pamac. 🖥️

---

## AppImage 🖼️

**AppImage** allows you to run applications as standalone executables without the need for installation or package management.

### How to Install AppImage Launcher 🛠️

To integrate AppImages with your system, install the AppImage Launcher:

```bash
sudo pacman -S appimagelauncher
```

### How to Use AppImage 📥

1. Download an AppImage from the web (e.g., [AppImageUpdate](https://appimage.github.io/AppImageUpdate)).
2. Double-click the AppImage file.
3. Choose whether to **integrate the app into your system** or **run it once**.

---

Happy package managing! 🎉💻
