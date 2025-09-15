---
title: 在 BredOS 上安装 STEAM
description: 一个在BredOS上安装Steam的简单指南，并对Panthorable和非Panthor的配置进行分步说明。
published: true
date: 2025-09-15T11:13:24.812Z
tags:
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 1. 简介

欢迎来到关于如何在 BredOS 上安装 **Steam** 的指南！ 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。

## 2. 必备条件

> 这是指Rockchip RK35xx 设备使用的操作！
> {.is-info}

- 您需要安装 **BredOS** 并运行。
- Optionally, you can have [Panthor enabled](/how-to/how-to-setup-panthor), but it's not required.

## 3. 安装步骤

### 3.1 自动使用

- 工具“bredos-config”提供了一个简单的方法来安装蒸汽和合适的蒸汽-libs。 启动工具为 启动工具为

```
sudo bredos-config
```

- 然后导航到 `Packages` -> `Install Steam` 。 然后，Steam将被安装。 简单，对吗？

### 3.2 手动处理

#### 3.2.1 如果使用旧的 BredOS 图像：

您可能需要添加 **BredOS Multilib** 仓库来安装 Steam 和必要的翻译层。 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤：

- 安装 `bredos-mullib` 包

```
   sudo pacman -S bredos-multilib
```

- 运行时更新软件包数据库：

```
   sudo pacman -Sy
```

#### 3.2.2 Steam安装：

- 运行以下命令来安装 Steam：

```
   sudo pacman -S steam
```

- 在执行命令后，您将看到一条消息，提示您选择一个选项。 选择基于您的配置的适当选项： 选择基于您的配置的适当选项： 选择基于您的配置的适当选项：

- 首先，选择 `lib32-vulkan-swrast`

![steam_libs_selection.png](/steam_libs_selection.png)

- 如果您已启用 **Panthor** ，请选择 `steam-libs-any`。

- 如果**Panthor** 未启用 (使用 Panfork 代替)，请选择 `steam-libs-rk3588`。

- 等待安装完成，你都已设置。

## 4. 正在卸载 Steam

- 如果您需要卸载 Steam 并重置配置以选择另一个选项：

```
sudo pacman -Rnscu steam steam-libs-any #or steam-libs-rk3588 取决于您的选择
```

## 5. 启动Steam

- 安装完成后，您可以通过在应用程序菜单中搜索或运行来启动Steam：

```
steam
```

> 快乐游戏！
> {.is-success}

