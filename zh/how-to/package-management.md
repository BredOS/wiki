---
title: 软件包管理指南
description: 欢迎使用 BredOS 软件包管理员指南！🚀 在这里，你会学习如何安装和管理应用程序。准备好控制您的系统应用！ 💻 在这里，您将学习如何安装和管理应用程序
published: true
date: 2025-09-15T09:53:59.847Z
tags:
editor: markdown
dateCreated: 2024-09-20T20：08：39.778Z
---

# 1. 简介

欢迎使用 BredOS 软件包管理员指南！🚀 在这里，你会学习如何安装和管理应用程序。 准备好控制您的系统应用！ 💻 在这里，您将学习如何安装和管理应用程序。 准备好控制您的系统应用！

# 2. Pacman

Pacman 是 BredOS 的默认软件包管理器，在管理软件包时以其速度和简洁性而闻名。

## 2.1 如何安装软件包

- 要与Pacman安装一个包，请使用以下命令：

```bash
sudo pacman -S <package name>
```

## 2.2 如何更新系统

- 要更新系统上所有已安装的软件包，请运行：

```bash
sudo pacman -Syu
```

这将同步软件包数据库并将您所有的软件包升级到他们的最新版本。

## 2.3 如何删除软件包

- 要卸载一个包，请使用：

```bash
sudo pacman -R <package name>
```

- 如果您想要删除一个软件包及其未使用的依赖，请运行：

```bash
sudo pacman -Rns <package name>
```

## 2.4 如何搜索软件包

- 要在 Pacman 仓库中搜索包，请使用：

```bash
pacman -Ss <package name>
```

## 2.5 检查已安装的软件包

- 要列出所有已安装的软件包，只需运行：

```bash
pacman -Q
```

## 2.6 清理缓存

- 要清理Pacman缓存并释放空间，请使用：

```bash
sudo pacman -Sc
```

> Pacman是管理您的 BredOS 系统的重要工具——迅速、高效和强大！
> {.is-success}
> {.is-success}

# 3. 平面板

Flatpak为运行应用程序提供一个沙盒环境，独立于主机系统的软件。

## 3.1 如何安装 Flatpak

- 要安装 Flatpak，请运行：

```bash
sudo pacman -S flatpak
```

> 安装Flatpak后可能需要重新启动您的系统。
> {.is-info}
> {.is-info}

## 3.2 从 Flahub 安装

### 3.2.1 通过Web浏览器安装应用程序

- 浏览到 [Flathub](https://flathub.org)，找到您想要的应用程序，然后点击安装。

![flathub-install-button.png](/how-tos/flathub-install-button.png)

### 3.2.2 通过终端安装应用程序

- 您也可以直接从终端安装应用程序：

```bash
sudo flatpak install <app name>
```

## 3.3 通过终端卸载应用

- 要删除应用，请运行：

```bash
sudo flatpak 卸载 <app name>
```

> 或者，您可以使用像Pamac这样的图形商店管理Flatpak应用。 🖥️ 🖥️
> {.is-info}
> {.is-info}

# 4. AppImage

AppImage 允许您以独立可执行文件运行应用程序，而无需安装或软件包管理。

## 4.1 如何安装 AppImage Launcher

- 若要将应用图像与您的系统集成，请安装 AppImage 启动器：

```bash
sudo pacman -S appimagelauncher
```

## 4.2 如何使用AppImage

- 从网上下载应用程序图像(如 [AppImageUpdate](https://appimage.github.io/AppImageUpdate))。
- 双击应用图像文件。
- 选择**将应用程序集成到您的系统**或者**一次运行**。

> 快乐的软件包管理！ 🎉💻 🎉💻
> {.is-success}
> {.is-success}

