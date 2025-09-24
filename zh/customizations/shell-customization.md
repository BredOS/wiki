---
title: BredOS Shell 定制指南 🐚🎨
description: 本指南将通过改变和提升你的 shell 体验来帮助你定制你的 BredOS 体验！🚀 无论你喜欢 Bash、Zsh、Fish 还是 Nushell，你都会在这里找到你需要的一切。让我们开始吧！🌊  无论你喜欢Bash、Zsh、Fish还是Nushell，你都会在这里找到你需要的一切。 让我们进去！ 🌊
published: true
date: 2025-09-16T10:37:25.923Z
tags: 自定义, shell
editor: markdown
dateCreated: 2024-09-20T19:39:08.509Z
---

# 1. Bash 🐢

本指南将通过改变和提升你的 shell 体验来帮助你定制你的 BredOS 体验！🚀 无论你喜欢 Bash、Zsh、Fish 还是 Nushell，你都会在这里找到你需要的一切。让我们开始吧！🌊  无论你喜欢Bash、Zsh、Fish还是Nushell，你都会在这里找到你需要的一切。 让我们进去！

# 2. Zsh ⚡

> Bash 是 BredOS 中的默认 shell。让我们开始设置它，或者使它成为你的默认 shell！
> {.is-info}

## 2.1 安装Zsh :hammer_and_wrench：

- 要安装 Bash，请运行：

```bash
sudo pacman -S bash
```

## 1.2 将Bash 设置为默认 Shell :gear：

- 要列出所有已安装的 shell，请运行：

```bash
chsh -l
```

- 设置 Bash 为您的默认 shell：

```bash
chsh -s /usr/bin/bash
```

注销并重新登录以开始使用 Bash 作为您的 shell。🔄 🔄

## 1.3 Oh My Bash 💡

通过 **Oh My Bash** 来提升 Bash，一个能够添加主题、插件和其它很酷的增强功能的框架！🌟

# 3. Fish 🐠

Zsh 是一个强大的 shell，具有许多先进的功能，使它比 Bash 更加灵活。

## 3.1 Install Zsh

- 要安装 Zsh，请运行：

```bash
sudo pacman -S zsh
```

## 3.2 功能 🌟

- **更好的制表符补全** ⌨️：Zsh 只在使用类似 `cd` 的命令时显示有效的目标。
- **更好的历史搜索** 🔍：键入之前命令的一部分，然后按 ⬆️ 在您的历史中搜索。

## 2.3 将Zsh设置为默认 Shell :gear：

- 要列出所有已安装的 shell，请运行：

```bash
chsh -l
```

- 设置 Zsh 为您的默认 shell：

```bash
chsh -s /usr/bin/zsh
```

注销并重新登录以切换到 Zsh！🔄

## 2.4 Oh 我的Zsh :cuble_scape：

**Oh My Zsh** 是一个社区驱动的框架，可以通过主题和插件增强 Zsh，让您拥有更强大的功能和灵活性。✨

# 4. Nushell 🧠

**Fish**（友好的交互式 shell）侧重于易于使用，具有开箱即用的强大功能。

## 3.1 安装 Fish :hammer_and_wrench：

- 要安装 Fish，请运行：

```bash
sudo pacman -S fish
```

## 4.2 功能 🌟

- **自动建议** 🤖：根据你的历史记录，Fish 会建议你输入的命令。
- **基于 Web 的配置** 🌐：通过 Web 界面自定义您的 shell 外观和行为。
- **开箱即用** 🧰：Tab 补全、语法高亮等功能无需额外设置！

## 3.3 设置鱼类为默认 Shell :gear：

- 要列出所有已安装的 shell，请运行：

```bash
chsh -l
```

- 设置 Fish 为您的默认 shell：

```bash
chsh -s /usr/bin/fish
```

注销并重新登录以享受 Fish！🔄

## 3.4 Oh My Fish 🎣

使用 **Oh My Fish** 添加插件和主题到 Fish，增强其功能和外观。🌈

# 5. 努舍尔

**Nushell** 对 shell 脚本采用现代方法，将所有输入视为结构化数据，使处理变得更容易。

## 5.1 安装 Nushell

- 要安装 Nushell，请运行：

```bash
sudo pacman -S nushell
```

## 2.2 功能 🌟

- **一切都是数据** 📊：Nu 管道处理结构化数据以便于筛选、排序和选择。
- **强大插件** 🔌：轻松地扩展 Nushell 和各种插件。
- **优秀的错误消息** 🛠️：Nushell 帮助您早期发现错误，并附有有用的错误消息。

## 4.3 设置Nushell为默认 Shell :gear：

- 要列出所有已安装的 shell，请运行：

```bash
chsh -l
```

- 设置 Nushell 为您的默认 shell：

```bash
chsh -s /usr/bin/nu
```

注销并重新登录以切换到 Nushell！🔄 🔄 🔄
