---
title: 主页
description:
published: true
date: 2025-10-04T09:42:23.478Z
tags:
editor: markdown
dateCreated: 2024-07-19T14:28:40.812Z
---

# 2. 🌟 概览

欢迎来到 BredOS 文档！BredOS 是一个基于 Arch 的用户友好型 Linux 发行版，专门为基于 ARM 的单板计算机（SBC）设计。
本文档将指导您完成 BredOS 的安装、配置和使用。 BredOS 是一个方便用户的基于档案的Linux发行版，专门为ARM和RISC-V设计的单个板电脑(SBC)。
文档将引导您安装、配置和使用 BredOS 。 BredOS 旨在为基于 ARM 的单板计算机用户提供无缝且用户友好的体验。 通过利用 Arch Linux 的强大功能和灵活性，BredOS 提供了一个可以根据广泛用例进行自定义的强大平台。
文档将引导您安装、配置和使用 BredOS 。

![boot-no-loop.gif](/boot-no-loop.gif)

# 3. 🚀 功能

- 我们运送功能安装，而不是配置。
- 无需体验。 这很简单；一切都有记录，[我们希望帮助](#h-7-community-and-support)！
- 设计简单明了！ 设计简单明了！ 没有博客，确保一个轻量和响应系统！
- 以存档为基础——专门设计用于打磨和易于使用的自定义系统。

## 2.1 特色工具

- Bakery - [your guide to your own Bred](/install/first-setup)!
- Bred-Tools - [你手上的swiss knife](/Tools)！
- Bed-配置 - [就像皮-config，但是有更好的味道！](/bredos-config)
- Govctl - [控制您的 CPU](/how-to/govctl) ！

# 🔁 3. 🛠️ 系统要求

我们支持一系列广泛的设备——从振奋人心的ARM系统和实验性RISC-V安装到普通旧的X86_64 整数/整数板上。 We've got you covered, whether you use our [mainline .iso installation](/en/install/Installation-with-ISO) or refer to the list of devices we passionately support on our [table of supported devices](/en/table-of-supported-devices).

## 3.1 最低限度制度要求

- **🧠 最小内存**：2 GB
- 存储: 8 GB microSD card/eMMC/NVMe 或大于

# 🚀 4. 刷入

我们的朋友[**DroidMaster**](https://www.youtube.com/@LinuxDroidMaster) 制作了一个关于BredOS的YouTube视频。 在这里查看： 在这里查看： 在这里查看：

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/eoLE27xdtu4?si=ai-0QqLNyCYfTKfA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# 🔄 3. 下载

您可以在我们的 [website](https://bredos.org/download.html) 中找到图像的下载链接！

# 5. 安装

为了便于您安装，我们为您铺设了一条线路，让您跟随。 🍞 🔸🔸🔸 🍞 🔸🔸🔸

## 5.1 设备特定图像安装

These are the boards we love the most. 这些是我们最喜欢的看板的图像。 要在它们上安装这个BredOS 图像，要么从我们的 [设备特定图像](/install/device-specific-image) 安装指南开始， 或者在我们wiki的设备页面上看一眼，这可以在这个页面的左侧导航栏找到。

访问我们的 [下载站点] (https://bredos.org/download.html) 来查找您的设备是否是其中之一。

## 5.2 通用安装

If your device isn’t listed on our [download site](https://bredos.org/download.html) but supports booting UEFI and is based on either x86_64- or ARM64 architecture, simply follow our guide for a generic installation available [here](/install/Installation-with-ISO).

## 5.3 码头集装箱安装

- 简易作为一行命令：

```
停靠拉入面包/bredos
```

# 4. 安装

查看此页面导航栏中的设备页面来查找您设备特有的问题。 如果您的问题没有列出在这里，请随时通过[我们的支持频道](#h-7-community-and-support)直接联系我们。

# 8. 🌐 社区和支持

BredOS 是一个开源项目，欢迎贡献！您可以通过以下方式做出贡献： 您可以通过以下方式做出贡献：

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhuyKXaa)
- [GitHub](http://github.com/BredOS)
  {.links-list}

# 9. 🤝 贡献

BredOS 是一个开源项目，欢迎贡献！您可以通过以下方式做出贡献： 您可以通过以下方式做出贡献： 您可以通过以下方式做出贡献： 您可以通过以下方式做出贡献：

- 🐛 报告错误和问题
- 💻 提交补丁和改进
- 📄 编写并改进文档
- 🧑‍🤝‍🧑 帮助其他用户在社区论坛和聊天

# 10. 主播活动

现在，RK3588设备的 BredOS 图像依赖结壳Rockchip BSP 内核——一个小屋。 管道录制的代码库很难维护、不安全，并且总是落后于上游Linux。

[我们想要更改那些](/en/internal-bred-stuff/mainline-campaign)。
