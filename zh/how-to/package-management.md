---
title: 📦✨ Package Managers Guide
description: "欢迎使用 BredOS 软件包管理员指南！ :rowt: 在这里，你会学习如何安装和管理应用程序。 准备好控制您的系统应用！ 💻 :ro火箭: 在这里，你会学习如何安装和管理应用程序"
published: true
date: 2024-09-20T20:10:47.203Z
tags: null
editor: markdown
dateCreated: 2024-09-20T20：08：39.778Z
---

# 📦✨ Package Managers Guide

欢迎使用 BredOS 软件包管理员指南！ :ro火箭: 在这里，你会学习如何安装和管理应用程序 :rowt: 在这里，你会学习如何安装和管理应用程序。 准备好控制您的系统应用！ 💻

---

## 📚 目录

- Pacman 🐧
- Flatpak 📦
- AppImage 🖼️

---

## Pacman 🐧

**Pacman** 是 BredOS 的默认软件包管理器，管理软件包时以其速度和简洁性著称。

### 如何安装软件包 🛠️

要与Pacman安装一个包，请使用以下命令：

```bash
sudo pacman -S <package name>
```

### 如何更新系统 :countrockwise_arrows_buton:

要更新系统上所有已安装的软件包，请运行：

```bash
sudo pacman -Syu
```

这将同步软件包数据库并将您所有的软件包升级到他们的最新版本。

### 如何删除软件包 :wastebacket:

要卸载一个包，请使用：

```bash
sudo pacman -R <package name>
```

如果您想要删除一个软件包及其未使用的依赖，请运行：

```bash
sudo pacman -Rns <package name>
```

### 如何搜索软件包 🔍

要在 Pacman 仓库中搜索包，请使用：

```bash
pacman -Ss <package name>
```

### 检查已安装的软件包 :剪贴板:

要列出所有已安装的软件包，只需运行：

```bash
pacman -Q
```

### 清除缓存 🧹

要清理Pacman缓存并释放空间，请使用：

```bash
sudo pacman -Sc
```

Pacman 是管理您的 BredOS 系统的重要工具。快速、高效和强大！ ⚡🐧 ⚡🐧

---

## Flatpak 📦

**Flatpak** 为运行应用程序提供一个沙盒环境，独立于主机系统的软件。

### 如何安装 Flatpak :hammer_and_wrench：

要安装 Flatpak，请运行：

```bash
sudo pacman -S flatpak
```

> **注意**：安装Flatpak后可能需要重新启动您的系统。 🔄 🔄

### 如何使用 Flatpak 📥

#### 从 Flathub :globe_with_meridians安装：

1. 浏览到 [Flathub](https://flathub.org)，找到您想要的应用程序，然后点击安装。
2. 复制终端中的命令来完成安装。

#### 通过 Terminal :keyboard 安装应用程序：

您也可以直接从终端安装应用程序：

```bash
sudo flatpak install <app name>
```

#### 通过 Terminal :wastebacket 卸载应用：

要删除应用，请运行：

```bash
sudo flatpak 卸载 <app name>
```

或者，您可以使用像Pamac这样的图形商店管理Flatpak应用。 🖥️ 🖥️

---

## AppImage 🖼️

**AppImage** 允许您以独立可执行文件运行应用程序，而无需安装或软件包管理。

### 如何安装AppImage Launcher :hammer_and_wrench：

若要将应用图像与您的系统集成，请安装 AppImage 启动器：

```bash
sudo pacman -S appimagelauncher
```

### 如何使用 AppImage 📥

1. 从网上下载应用程序图像(如 [AppImageUpdate](https://appimage.github.io/AppImageUpdate))。
2. 双击应用图像文件。
3. 选择**将应用程序集成到您的系统**或者**一次运行**。

---

快乐的软件包管理！ 🎉💻 🎉💻
