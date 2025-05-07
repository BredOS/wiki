---
title: 使用 DTSC
description: 使用 BredOS 设备树源编译器辅助脚本
published: true
date: 2025-05-07T13：18：58.737Z
tags: null
editor: markdown
dateCreated: 2025-05-07T13：18：58.736Z
---

# DTSC

`dtsc` 是一个默认与BredOS和`breddos-tools`软件包一起发送的命令。
但要让它起作用，你需要安装 `dtc`，只需运行 `yay -S dtc`

脚本是一个 dtsc, 执行自动的 gcc 预处理, 链接和生成所需文件.
它使得设备树的生成和测试大为简化。
它自动决定并生成基础设备树或叠加层。

## 导入笔记

**在您的设备上安装不正确的设备树将使它无法操作。**
**小心，执行备份并确保一个应急计划。**