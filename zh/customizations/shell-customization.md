---
title: "BredOS Shell 定制指南 🐚:artist_调色板:"
description: "本指南将通过改变和提升你的壳体验来帮助你定制你的 BredOS 体验！ :ro火箭: 无论你喜欢Bash、Zsh、Fish还是Nushell, 你都会在这里找到你需要的一切。 让我们进去！ 🌊 :ro火箭: 无论你喜欢Bash、Zsh、Fish还是Nushell, 你都会在这里找到你需要的一切。 让我们进去！ 🌊"
published: true
date: 2024-09-21T09:02:20.084Z
tags: 自定义化 shell
editor: markdown
dateCreated: 2024-09-20T19：39：08.509Z
---

# BredOS Shell 定制指南 🐚:artist_调色板:

本指南将通过改变和提升你的壳体验来帮助你定制你的 BredOS 体验！ :ro火箭: 无论你喜欢Bash、Zsh、Fish还是Nushell, 你都会在这里找到你需要的一切。 让我们进去！ 🌊 :ro火箭: 无论你喜欢Bash、Zsh、Fish还是Nushell, 你都会在这里找到你需要的一切。 让我们进去！ 🌊

---

## 📚 目录

- Bash :turt:
- Zsh ⚡
- 鱼：热带鱼：
- Nushell 🧠

---

## Bash :turt:

Bash 是 BredOS 中的默认外壳。 让我们开始设置它，或者使它成为你的默认外壳！ 让我们开始设置它，或者使它成为你的默认外壳！

### 安装 Bash :hammer_and_wrench：

要安装 Bash，请运行：

```bash
sudo pacman -S bash
```

### Bash 设置为默认 Shell :gear：

1. 要列出所有已安装的外壳，请运行：
   ```bash
   块-l
   ```
2. 设置Bash为您的默认外壳：
   ```bash
   chsh -s /usr/bin/bash
   ```
3. 注销并重新登录以开始使用 Bash 作为您的外壳。 🔄 🔄

### Oh My Bash 💡

通过 **Oh My Bash**来提升Bash ，一个能够添加主题、插件和其它很酷的增强功能的框架！ 🌟 🌟

---

## Zsh ⚡

Zsh是一个强大的炮弹，具有许多先进的功能，使它比巴希更能多变通。

### 安装 Zsh :hammer_and_wrench：

要安装 Zsh，请运行：

```bash
sudo pacman -S zsh
```

### 功能 🌟

- **更好的制表符完成** ⌨️: Zsh只在使用类似`cd`的命令时显示有效的目的地。
- **Better History Search** 🔍: 键入之前命令的一部分，然后按 ⬆️ 在您的历史中搜索。

### Oh 我的Zsh :cuble_scape：

**Oh My Zsh** 是一个社区驱动的框架，可以通过主题和插件增强Zsh，让您拥有更大的力量和灵活性。 ✨ ✨

### 将Zsh设置为默认 Shell :gear：

1. 要列出所有已安装的外壳，请运行：
   ```bash
   块-l
   ```
2. 设置Zsh为您的默认外壳：
   ```bash
   chsh -s /usr/bin/zsh
   ```
3. 注销并重新登录以切换到Zsh！ 🔄 🔄

---

## 鱼：热带鱼：

**Fish** (友好的交互式贝壳) 侧重于易于使用，具有来自箱子的巨大功能。

### 安装 Fish 🛠️

要安装鱼类，请运行：

```bash
sudo pacman -S fish
```

### 功能 🌟

- **自动建议** 🤖: 根据你的历史记录, 鱼类表示你类型的命令。
- **基于Web的配置** 🌐: 通过 Web 界面自定义您的 shell 外观和行为。
- **运行于箱子** 🧰: Tab 补全, 语法高亮, 以及更多没有额外设置!

### 哦我的鱼:fishing_pole：

使用 **Oh 我的鱼类** 添加插件和主题到鱼类，增强其功能和美术。 🌈 🌈

### 设置鱼类为默认 Shell :gear：

1. 要列出所有已安装的外壳，请运行：
   ```bash
   块-l
   ```
2. 设置鱼类为您的默认外壳：
   ```bash
   chsh -s /usr/bin/fish
   ```
3. 注销并重新登录以享受鱼类！ 🔄 🔄

---

## Nushell 🧠

**Nushell** 对shell 脚本采取现代方法，将所有输入视为结构化数据，使处理变得更容易。

### 安装Nushell:hammer_and_wrench：

要安装 Nushell，请运行：

```bash
sudo pacman -S nushell
```

### 功能 🌟

- **一切都是数据** 📊: Nu 管道处理结构化数据以便于筛选、排序和选择。
- **强大插件** :electric_plugs:: 轻松地扩展Nushell和各种插件。
- **优秀的错误消息** 🛠️: Nushell帮助您在早期发现错误，并附有有用的错误消息。

### 设置Nushell为默认 Shell :gear：

1. 要列出所有已安装的外壳，请运行：
   ```bash
   块-l
   ```
2. 设置Nushell为您的默认外壳：
   ```bash
   chsh -s /usr/bin/nu
   ```
3. 注销并重新登录以切换到Nushell！ 🔄 🔄
