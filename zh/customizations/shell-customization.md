---
title: BredOS Shell 自定义指南
description: 本指南将通过改变和提升你的 shell 体验来帮助你定制你的 BredOS 体验！🚀 无论你喜欢 Bash、Zsh、Fish 还是 Nushell，你都会在这里找到你需要的一切。让我们开始吧！🌊  无论你喜欢Bash、Zsh、Fish还是Nushell，你都会在这里找到你需要的一切。 让我们进去！ 🌊
published: true
date: 2025-09-16T10:37:25.923Z
tags: 自定义, shell
editor: markdown
dateCreated: 2024-09-20T19:39:08.509Z
---

# 1. 简介

本指南将通过改变和提升你的 shell 体验来帮助你定制你的 BredOS 体验！🚀 无论你喜欢 Bash、Zsh、Fish 还是 Nushell，你都会在这里找到你需要的一切。让我们开始吧！🌊  无论你喜欢Bash、Zsh、Fish还是Nushell，你都会在这里找到你需要的一切。 让我们进去！

# 2. 巴什文

> Bash 是 BredOS 中的默认 shell。让我们开始设置它，或者使它成为你的默认 shell！
> {.is-info}

让我们开始设置它或制作你的默认炮弹！

## 2.1 安装 Bash

- 要安装 Bash，请运行：

```bash
sudo pacman -S bash
```

## 2.2 将Bash 设置为默认 Shell

- 要列出所有已安装的 shell，请运行：

```bash
   块-l
```

- 设置 Bash 为您的默认 shell：

```bash
   chsh -s /usr/bin/bash
```

注销并重新登录以开始使用 Bash 作为您的 shell。🔄

## 2.3 Oh 我的Bash

通过 **Oh My Bash** 来提升 Bash，一个能够添加主题、插件和其它很酷的增强功能的框架！🌟

# 3. 兹什文

Zsh 是一个强大的 shell，具有许多先进的功能，使它比 Bash 更加灵活。

## 3.1 Install Zsh

- 要安装 Zsh，请运行：

```bash
sudo pacman -S zsh
```

## 3.2 特点

- **更好的Tab 补全**：Zsh 只在使用类似`cd`的命令时显示有效的目的地。
- **更好的历史搜索**：输入前一个命令的一部分，然后按 :up_arrow：进行历史搜索。

## 3.3 将Zsh设置为默认Shell

- 要列出所有已安装的 shell，请运行：

```bash
   块-l
```

- 设置 Zsh 为您的默认 shell：

```bash
   chsh -s /usr/bin/zsh
```

注销并重新登录以切换到 Zsh！🔄

## 3.4 Oh My Zsh

**Oh My Zsh** 是一个社区驱动的框架，可以通过主题和插件增强 Zsh，让您拥有更强大的功能和灵活性。✨

# 4. 鱼类

**Fish**（友好的交互式 shell）侧重于易于使用，具有开箱即用的强大功能。

## 4.1 安装 Fish

- 要安装 Fish，请运行：

```bash
sudo pacman -S fish
```

## 4.2 功能

- **自动建议**：根据您的历史，鱼类表示你类型的命令。
- **基于网络的配置**：通过网页界面自定义您的 shell 外观和行为。
- **超越盒子**：制表符完成、语法高亮以及更多没有额外设置！

## 4.3 设置鱼类为默认 Shell

- 要列出所有已安装的 shell，请运行：

```bash
   块-l
```

- 设置 Fish 为您的默认 shell：

```bash
   chsh -s /usr/bin/fish
```

注销并重新登录以享受 Fish！🔄

## 4.4 Oh My Fish

使用 **Oh My Fish** 添加插件和主题到 Fish，增强其功能和外观。🌈

# 5. 努舍尔

**Nushell** 对 shell 脚本采用现代方法，将所有输入视为结构化数据，使处理变得更容易。

## 5.1 安装 Nushell

- 要安装 Nushell，请运行：

```bash
sudo pacman -S nushell
```

## 5.2 功能

- **一切都是数据**：Nu 管道处理结构化数据以便于筛选、排序和选择。
- **强大的插件**: 轻松扩展Nushell和各种插件。
- **优秀的错误消息**：Nushell帮助您及早发现错误，并附有有用的错误消息。

## 5.3 将Nushell设置为默认 Shell

- 要列出所有已安装的 shell，请运行：

```bash
   块-l
```

- 设置 Nushell 为您的默认 shell：

```bash
   chsh -s /usr/bin/nu
```

注销并重新登录以切换到 Nushell！🔄 🔄
