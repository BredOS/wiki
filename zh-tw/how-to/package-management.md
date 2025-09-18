---
title: Package Managers Guide
description: Welcome to the BredOS Package Managers guide! Here, you'll learn how to install and manage applications
published: true
date: 2025-09-15T09:53:59.847Z
tags:
editor: markdown
dateCreated: 2024-09-20T20:08:39.778Z
---

# 1. 簡介

Welcome to the BredOS Package Managers guide! Here, you'll learn how to install and manage applications. Get ready to take control of your system's apps!

# 2. Pacman

Pacman is the default package manager for BredOS, known for its speed and simplicity when managing software packages.

## 2.1 How to Install Packages

- 要使用 Pacman 安裝軟件包，請使用以下命令：

```bash
sudo pacman -S <package name>
```

## 2.2 How to Update the System

- To update all installed packages on your system, run:

```bash
sudo pacman -Syu
```

This will synchronize the package databases and upgrade all your packages to their latest versions.

## 2.3 How to Remove Packages

- 要卸載軟件包，請使用：

```bash
sudo pacman -R <package name>
```

- 如果您想移除軟件包及其未使用的依賴項，請運行：

```bash
sudo pacman -Rns <package name>
```

## 2.4 How to Search for Packages

- 要在 Pacman 儲存庫中搜索軟件包，請使用：

```bash
pacman -Ss <package name>
```

## 2.5 Check Installed Packages

- To list all installed packages, simply run:

```bash
pacman -Q
```

## 2.6 Clear Cache

- To clear the Pacman cache and free up space, use:

```bash
sudo pacman -Sc
```

> Pacman is an essential tool for managing your BredOS system — quick, efficient, and powerful!
> {.is-success}

# 3. Flatpak

Flatpak provides a sandboxed environment for running applications, independent of the host system’s software.

## 3.1 How to Install Flatpak

- To install Flatpak, run:

```bash
sudo pacman -S flatpak
```

> It may be necessary to reboot your system after installing Flatpak.
> {.is-info}

## 3.2 Install from Flathub

### 3.2.1 Install an App via the Webbrowser

- Navigate to [Flathub](https://flathub.org), find the app you want, and click install.
- Copy the command in the terminal to complete the installation.

### 3.2.2 Install an App via Terminal

- You can also install apps directly from the terminal:

```bash
sudo flatpak install <app name>
```

## 3.3 Uninstall an App via Terminal

- To remove an app, run:

```bash
sudo flatpak uninstall <app name>
```

> Alternatively, you can manage Flatpak apps using a graphical store like Pamac.
> {.is-info}

# 4. AppImage

AppImage allows you to run applications as standalone executables without the need for installation or package management.

## 4.1 How to Install AppImage Launcher

- To integrate AppImages with your system, install the AppImage Launcher:

```bash
sudo pacman -S appimagelauncher
```

## 4.2 How to Use AppImage

- Download an AppImage from the web (e.g., [AppImageUpdate](https://appimage.github.io/AppImageUpdate)).
- Double-click the AppImage file.
- Choose whether to **integrate the app into your system** or **run it once**.

> Happy package managing!
> {.is-success}

