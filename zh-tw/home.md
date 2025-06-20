---
title: BredOS 主頁
description:
published: true
date: 2024-07-19T14:36:23.702Z
tags:
editor: markdown
dateCreated: 2024-07-19T14:36:23.702Z
---

# 🍞 The BredOS Wiki

## 🌟 Overview

歡迎來到 BredOS 文檔！ BredOS 是一個基於 Arch 的用戶友好型 Linux 發行版，專門為基於 ARM 的單板計算機（SBC）設計。
The documentation will guide you through the installation, configuration, and usage of BredOS.

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

## 📚 Table of Contents

1. [🔍 Introduction](#introduction)
2. [🚀 Features](#features)
3. [🛠️ System Requirements](#system-requirements)
4. [💽 Installation](/installation)
5. [📦 Package Management](#package-management)
6. [🐞 Troubleshooting](#troubleshooting)
7. [❓FAQ](#faq)
8. [🌐 Community and Support](#community-and-support)
9. [🤝 Contributing](#contributing)

## 🔍 Introduction

BredOS 旨在為基於 ARM 的單板計算機用戶提供無縫且用戶友好的體驗。 通過利用 Arch Linux 的強大功能和靈活性，BredOS 提供了一個可以根據廣泛用例進行自定義的強大平台。

## 🚀 Features

- **🖥️ User-Friendly Interface**: A simplified and intuitive user interface for easy navigation and use.
- **🎯 Arch-Based**: Built on top of Arch Linux, ensuring access to a vast repository of packages and a rolling release model.
- **🔧 ARM Support**: Optimized for ARM-based single board computers, making it ideal for devices like the Rock 5B, and more.
- **⚡ Lightweight**: Minimal bloat, ensuring a lightweight and responsive system.

## 🛠️ System Requirements

- **🖥️ Supported Devices**:
  - Radxa Rock 5 A/B/C
  - Radxa Rock 4 C
  - Radxa NX5 Kit
  - IndieDroid Nova
  - Orange Pi 5/5+
  - Khadas Edge 2
  - Khadas VIM 4
  - Cool Pi 4B
  - [Fydetab Duo](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/blob/main/Documentation/Linux_distros/bredos.md)
- **🧠 Minimum RAM**: 2 GB
- **💾 Storage**: 16 GB microSD card or larger
- **🌐 Network**: Optional

## 💽 Installation

請參閱我們的 [安裝指南](/installation) 頁面以獲取更多信息。

## 📦 Package Management

BredOS 使用 `pacman`，這是來自 Arch Linux 的軟件包管理器。 以下是一些常用命令：

- 🔄 Update package list: `sudo pacman -Syu`
- ➕ Install a package: `sudo pacman -S [package_name]`
- ➖ Remove a package: `sudo pacman -R [package_name]`
- 🔍 Search for a package: `pacman -Ss [package_name]`

## 🐞 Troubleshooting

如果您遇到 BredOS 的問題，歡迎加入我們的 [Discord](https://discord.gg/jwhxuyKXaa) 進行咨詢。

## ❓ FAQ

### ❓ Q: What devices are supported by BredOS?

A: BredOS supports a variety of ARM-based single board computers, the complete list is available at [supported devices](#system-requirements).

### 🔄 Q: How do I update BredOS?

答：您可以使用 `pacman` 軟件包管理器通過命令 `sudo pacman -Syu` 更新 BredOS。

### 📦 Q: Where can I find additional software packages?

答：您可以在 Arch 用戶倉庫（AUR）中找到額外的軟件包，並使用 `yay` 或 `paru` 安裝它們。

### Q: The power consumption of my device is high, how can I reduce it?

A: You can reduce the power consumption by changing the CPU governor to `ondemand` or `conservative` by editing the `/etc/default/cpupower` file.

### Q: The suspend is not working.

A: Please make sure that:

- Don't suspend before 10s after just  resuming, this is a known issue with the eMMC driver.
- Don't setup "suspend" as the action for the power button, because it will suspend the device immediately after resuming! (This will cause the device to enter a resume-suspend loop!)

## 🌐 Community and Support

加入 BredOS 社區，獲取支持、分享想法並為項目做出貢獻：

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhxuyKXaa)
- [💻 GitHub](http://github.com/BredOS)

## 🤝 Contributing

BredOS 是一個開源項目，歡迎貢獻 您可以通過以下方式進行貢獻：

- 🐛 Report bugs and issues
- 💻 Submit patches and improvements
- 📄 Write and improve documentation
- 🧑‍🤝‍🧑 Help other users in the community forums and chat

For more information on contributing, visit our [💻 GitHub](http://github.com/BredOS) or you can message us on [💬 Discord](https://discord.gg/jwhxuyKXaa) or join our [📱 Telegram](https://t.me/bredoslinux).
