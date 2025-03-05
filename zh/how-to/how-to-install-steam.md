---
title: 🎮 如何在 BredOS 上安装 STEAM
description: 一个在BredOS上安装Steam的简单指南，并对Panthorable和非Panthor的配置进行分步说明。
published: true
date: 2024-09-08T10:37:48.498Z
tags: null
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 🎮 如何在 BredOS 上安装 Steam

欢迎来到关于如何在 BredOS 上安装 **Steam** 的指南！ 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。

## 🛠️ 前提条件

> 注意：Steam似乎只能在 X11 桌面上工作。 此外，它可能无法在所有设备上运行(主要是非RK3588设备)。
> {.is-info} 此外，它可能无法在所有设备上运行(主要是非RK3588设备)。
> {.is-info} 此外，它可能无法在所有设备上运行(主要是非RK3588设备)。
> {.is-info}

- 您需要安装 **BredOS** 并运行。
- 可选，您可以启用 [**Panthor** ](/en/how-to/how to setup-panthor)，但不需要它。

## 📥 安装步骤

### :countrockwise_arrows_buton: 如果使用旧的 BredOS 图像：

您可能需要添加 **BredOS Multilib** 仓库来安装 Steam 和必要的翻译层。 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤：

1. 安装 `bredos-mullib` 包

```
   sudo pacman -S bredos-multilib
```

2. 运行时更新软件包数据库：

```
   sudo pacman -Sy
```

---

### :desktop_compute: Steam安装:

1. 打开您的终端 :desktop_compute:。
2. 运行以下命令来安装 Steam：

```
   sudo pacman -S steam
```

3. 在执行命令后，您将看到一条消息，提示您选择一个选项。 选择基于您的配置的适当选项： 选择基于您的配置的适当选项： 选择基于您的配置的适当选项：

   - 首先，选择 `lib32-vulkan-swrast`

![steam_libs_selection.png](/steam_libs_selection.png)

- 如果您已启用 **Panthor** ，请选择 `steam-libs-any`。
- 如果**Panthor** 未启用 (使用 Panfork 代替)，请选择 `steam-libs-rk3588`。

4. 等待安装完成，你都设置了！ 🎉 🎉 🎉

## :countrockwise_arrows_buton: 卸载 Steam

如果您需要卸载 Steam 并重置配置以选择另一个选项：

```
sudo pacman -Rnscu steam steam-libs-any #or steam-libs-rk3588 取决于您的选择
```

## :ro火箭：发射Steam

安装完成后，您可以通过在应用程序菜单中搜索或运行来启动Steam：

```
steam
```

**快乐游戏！ 🎮✨** 🎮✨\*\* 🎮✨\*\*
