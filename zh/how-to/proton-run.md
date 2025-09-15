---
title: 正在运行
description: 快速解释使用 BredOS `proton-run` 脚本
published: true
date: 2025-09-15T09:55:16.279Z
tags:
editor: markdown
dateCreated: 2025-05-07T14：44：47.710Z
---

# 1. 简介

`proton-run` 是一个最近发布的软件包，它允许您使用Steam的质子实验在BredOS ARM64下运行x86_64 Windows 应用程序。

# 2. B. 所需经费

- An RK3588 system running BredOS.
- Steam。 Steam。 Steam。 ([Guide here](/how-to/how-to-install-steam))

# 3. 安装

## 3.1 安装Steam的质子测试

打开Steam并导航到您的`Library`。 单击搜索栏并输入 `proton` 。 选择 `Proton Experimental` 并安装它。

> 其他版本的质子将不起作用。
> {.is-info}

## 3.2 安装质子运行

- 使用 `proton-run`

```
yay -S Proton-运行
```

# 4. 用法

- 只需打开终端并运行：

```
proton-run /path/to/your/windows/program.exe
```

> 不会有很多应用正常工作。 有三个仿真器链来使这成为可能。
> 但是它是x86的仿真状态。
> {.is-warning}
