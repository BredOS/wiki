---
title: 正在运行
description: 快速解释使用 BredOS `proton-run` 脚本
published: true
date: 2025-09-13T09:47:37.755Z
tags:
editor: markdown
dateCreated: 2025-05-07T14：44：47.710Z
---

# 使用 Proton-run 来运行窗口应用

工具`protonrun` 是一个最近发布的软件包，允许您使用 Steam 的质子实验在 BredOS ARM64 下运行 x86_64 Windows 应用程序。

## 1. B. 所需经费

- An RK3588 system running BredOS.
- Steam。 Steam。 ([Guide here](/how-to/how-to-install-steam))

## 2. 安装

### 2.1 安装Steam的质子测试

打开Steam并导航到您的`Library`。 单击搜索栏并输入 `proton` 。 选择 `Proton Experimental` 并安装它。 其他版本的质子将不起作用。

### 2.2 安装Proton-运行

用命令安装 `proton-run`

```
yay -S Proton-运行
```

## 3. 用法

只需打开终端并运行：

```
proton-run /path/to/your/windows/program.exe
```

> 不会有很多应用正常工作。 有三个仿真器链来使这成为可能。
> 但是它是x86的仿真状态。
> {.is-warning}
