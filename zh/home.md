---
title: 目录
description: null
published: true
date: 2024-08-16T18:32:54.710Z
tags: null
editor: markdown
dateCreated: 2024-07-19T14:28:40.812Z
---

# 🍞 BredOS Wiki

## 🌟 概览

BredOS 主页 欢迎来到 BredOS 文档！BredOS 是一个基于 Arch 的用户友好型 Linux 发行版，专门为基于 ARM 的单板计算机（SBC）设计。本文档将指导您完成 BredOS 的安装、配置和使用。
文档将引导您安装、配置和使用 BredOS 。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

## :books：目录表

1. [🔍 Introduction](#introduction)
2. [:ro火箭: 特征](#功能)
3. [🛠️ 系统要求](#system-requirements)
4. [:coly_disk: 安装](/install)
5. [📦 Package Management](#package-management)
6. [🐞 疑难解答](#troubleshooting)
7. [❓FAQ](#faq)
8. [:globe_with_meridian: Community and Support](#community and-support)
9. [🤝 贡献](#贡献)

## :magnifying_glass_tilted_left：介绍

BredOS 旨在为基于 ARM 的单板计算机用户提供无缝且用户友好的体验。通过利用 Arch Linux 的强大功能和灵活性，BredOS 提供了一个可以根据广泛用例进行自定义的强大平台。 通过利用 Arch Linux 的强大功能和灵活性，BredOS 提供了一个可以根据广泛用例进行自定义的强大平台。

## :ro火箭: 功能

- **:desktop_compute: 用户友好界面**: 简化和直观的用户界面以方便导航和使用。
- **🎯 Arch-Based**: 建立在Arch Linux顶部，以确保访问一个庞大的软件包仓库和滚动版本模型。
- **🔧 ARM Support**: 优化基于ARM的单个板电脑，使它适合于像Rock 5B等设备。
- **:high_voltage：浅色**：最小的博客，确保一个轻量和响应系统。

## 🛠️ 系统要求

- **:desktop_compute: 支持的设备**:
  - Radxa Rock 5 A/B/C
  - Radxa Rock 4 C
  - Radxa NX5 套件
  - IndieDroid Nova
  - 橙色Pi 5/5+
  - Khadas Edge 2
  - Khadas VIM 4
  - 酷皮4B
  - [FydetabDuo](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/blob/main/Documentation/Linux_distros/bredos.md)
- **🧠 最小内存**: 2 GB
- **💾 Storage**: 16 GB microSD card 或大于
- **🌐 Network**: 可选的

## :coly_disk: 安装

请参阅我们的 [安装指南](/installation) 页面以获取更多信息。

## 📦 包管理

BredOS 使用 `pacman`，这是来自 Arch Linux 的软件包管理器。以下是一些常用命令： 以下是一些常见的命令：

- :countrockwise_arrows_button: 更新包列表: `sudo pacman -Syu`
- ➕ Install a package: `sudo pacman -S [package_name]`
- ➖ 移除一个包: `sudo pacman -R [package_name]`
- 🔍 搜索包: `pacman -Ss [package_name]`

## :lady_beetle：故障排行

如果您遇到 BredOS 的问题，欢迎加入我们的 [Discord](https://discord.gg/jwhxuyKXaa) 进行咨询。

## ❓ 常见问题

### ❓ Q: BredOS支持哪些设备？

甲：BredOS 支持各种基于ARM的单个板电脑，完整列表可在 [支持的设备](#system-requires)。

### :countrockwise_arrows_buton: Q: 我如何更新 BredOS?

答：您可以使用 `pacman` 软件包管理器通过命令 `sudo pacman -Syu` 更新 BredOS。

### 📦 Q: 我可以在哪里找到其他软件包？

答：您可以在 Arch 用户仓库（AUR）中找到额外的软件包，并使用 `yay` 或 `paru` 安装它们。

## 🌐 社区和支持

加入 BredOS 社区，获取支持、分享想法并为项目做出贡献：

- [📱 Telegram](https://t.me/bredoslinux)
- [:speech_balon: Discord](https://discord.gg/jwhuyKXaa)
- [💻 GitHub](http://github.com/BredOS)

## :handshake：贡献

BredOS 是一个开源项目，欢迎贡献！您可以通过以下方式进行贡献： 您可以通过以下方式做出贡献：

- :bug : 报告 bug 和问题
- 💻 提交补丁和改进
- 📄 写入并改进文档
- 🧑‍🤝‍🧑 帮助其他用户在社区论坛和聊天

欲了解更多关于贡献的信息，请访问我们的 [💻 GitHub](http://github.com/BredOS)或您可以在 [:speech_clanon: Discord](https://discord.gg/jwhuyKXa) 或加入我们的 [📱 Telegram](https://t.me/breddoslinux)。
