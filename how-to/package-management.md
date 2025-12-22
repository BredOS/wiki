---
title: Package Managers Guide
description: Welcome to the BredOS Package Managers guide! Here, you'll learn how to install and manage applications
published: true
date: 2025-12-22T06:22:03.605Z
tags: 
editor: markdown
dateCreated: 2024-09-20T20:08:39.778Z
---

# 1. Introduction

Welcome to the BredOS Package Managers guide! Here, you'll learn how to install and manage applications. Get ready to take control of your system's apps!


# 2. Pacman
Pacman is the default package manager for BredOS, known for its speed and simplicity when managing software packages.

## 2.1 How to Install Packages
- To install a package with Pacman, use the following command:
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
- To uninstall a package, use:
```bash
sudo pacman -R <package name>
```
- If you want to remove a package and its unused dependencies, run:
```bash
sudo pacman -Rns <package name>
```

## 2.4 How to Search for Packages
- To search for a package in the Pacman repositories, use:
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

## 2.7 Reset TrustDB
If you have problems to install any package, because of the error `error: keyring: signature from "<name of signer here>" is unknown trust`, resetting the database containing the signature keys for pacman and rebuilding it, fixes it.

- To remove the old database, run:
```
sudo rm -rf /etc/pacman.d/gnupg
```

- Then rebuild your database with:
```
sudo pacman-key --init
sudo pacman-key --populate
```


> Pacman is an essential tool for managing your BredOS system — quick, efficient, and powerful!
{.is-success}


# 3. Flatpak
Flatpak provides a sandboxed environment for running applications, independent of the host system’s software.

## 3.1 How to Install Flatpak
- To install Flatpak, run:
```bash
sudo pacman -S flatpak
```
> It may be necessary to reboot your system after installing Flatpak.
{.is-info}

## 3.2 Install from Flathub
### 3.2.1 Install an App via the Webbrowser
- Navigate to [Flathub](https://flathub.org), find the app you want, and click install.

![flathub-install-button.png](/how-tos/flathub-install-button.png)
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
> 
> Alternatively, you can manage Flatpak apps using a graphical store like Pamac.
{.is-info}



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

> 
> Happy package managing!
{.is-success}

