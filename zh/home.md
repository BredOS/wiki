---
title: 主页
description:
published: true
date: 2024-07-19T14:28:40.812Z
tags:
editor: markdown
dateCreated: 2024-07-19T14:28:40.812Z
---

# 🍞 BredOS Wiki

## 🌟 概览

欢迎来到 BredOS 文档！BredOS 是一个基于 Arch 的用户友好型 Linux 发行版，专门为基于 ARM 的单板计算机（SBC）设计。
本文档将指导您完成 BredOS 的安装、配置和使用。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

## 📚 目录

1. [🔍 简介](#简介)
2. [🚀 功能](#功能)
3. [🛠️ 系统要求](#系统要求)
4. [💽 安装](/installation)
5. [📦 包管理](#包管理)
6. [🐞 疑难解答](#疑难解答)
7. [❓ 常见问题](#常见问题)
8. [🌐 社区与支持](#社区与支持)
9. [🤝 贡献](#贡献)

## 🔍 简介

BredOS 旨在为基于 ARM 的单板计算机用户提供无缝且用户友好的体验。通过利用 Arch Linux 的强大功能和灵活性，BredOS 提供了一个可以根据广泛用例进行自定义的强大平台。

## 🚀 功能

- **🖥️ 用户友好界面**：简化和直观的用户界面以方便导航和使用。
- **🎯 基于 Arch**：建立在 Arch Linux 之上，以确保访问一个庞大的软件包仓库和滚动发布模型。
- **🔧 ARM 支持**：优化基于 ARM 的单板计算机，使它适合于像 Rock 5B 等设备。
- **⚡ 轻量级**：最小化冗余，确保系统轻量且响应迅速。

## 🛠️ 系统要求

- **🖥️ 支持的设备**：
  - Radxa Rock 5 A/B/C
  - Radxa Rock 4 C
  - Radxa NX5 套件
  - IndieDroid Nova
  - Orange Pi 5/5+
  - Khadas Edge 2
  - Khadas VIM 4
  - Cool Pi 4B
  - [FydetabDuo](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/blob/main/Documentation/Linux_distros/bredos.md)
- **🧠 最小内存**：2 GB
- **💾 存储**：16 GB 或更大的 microSD 卡
- **🌐 网络**：可选

## 💽 安装

请参阅我们的 [安装指南](/installation) 页面以获取更多信息。

## 📦 包管理

BredOS 使用 `pacman`，这是来自 Arch Linux 的软件包管理器。以下是一些常见的命令：

- 🔄 更新软件包列表：`sudo pacman -Syu`
- ➕ 安装包：`sudo pacman -S [package_name]`
- ➖ 移除包：`sudo pacman -R [package_name]`
- 🔍 搜索包：`pacman -Ss [package_name]`

## 🐞 故障排除

如果您遇到 BredOS 的问题，欢迎加入我们的 [Discord](https://discord.gg/jwhxuyKXaa) 进行咨询。

## ❓ 常见问题

### ❓ Q: BredOS 支持哪些设备？

A：BredOS 支持各种基于 ARM 的单板计算机，完整列表可在[系统要求](#系统要求)中找到。

### 问：如何更新 BredOS？

答：您可以使用 `pacman` 软件包管理器通过命令 `sudo pacman -Syu` 更新 BredOS。

### 📦 Q: 我可以在哪里找到其他软件包？

答：您可以在 Arch 用户仓库（AUR）中找到额外的软件包，并使用 `yay` 或 `paru` 安装它们。

### 问：我的设备耗电量很高，我如何减少它？

A：您可以通过编辑 `/etc/default/cpupower` 文件将 CPU 调节器更改为 `ondemand` 或 `conservative` 来降低电量消耗。

### 问：暂停不起作用。

A：请确保：

- 刚刚恢复 10 秒前不要暂停，这是一个已知的 eMMC 驱动问题。
- 不要设置"暂停"作为电源按钮的动作，因为它会在恢复后立即暂停设备！（这将会导致设备进入恢复暂停循环！）

## 🌐 社区和支持

加入 BredOS 社区，获取支持、分享想法并为项目做出贡献：

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhuyKXaa)
- [💻 GitHub](http://github.com/BredOS)

## 🤝 贡献

BredOS 是一个开源项目，欢迎贡献！您可以通过以下方式做出贡献：

- 🐛 报告错误和问题
- 💻 提交补丁和改进
- 📄 编写并改进文档
- 🧑‍🤝‍🧑 帮助其他用户在社区论坛和聊天

欲了解更多关于贡献的信息，请访问我们的 [💻 GitHub](http://github.com/BredOS) 或您可以在 [💬 Discord](https://discord.gg/jwhxuyKXaa) 或加入我们的 [📱 Telegram](https://t.me/bredoslinux)。
