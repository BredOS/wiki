---
title: 正在运行
description: 快速解释使用 BredOS `proton-run` 脚本
published: true
date: 2025-05-07T14：44：47.710Z
tags: null
editor: markdown
dateCreated: 2025-05-07T14：44：47.710Z
---

# 使用 `proton-run`

`proton-run` 是一个最近发布的软件包，它允许您使用Steam的质子实验在BredOS ARM64下运行x86_64 Windows 应用程序。

## B. 所需经费

- An RK3588 system running BredOS.
- Steam。 ([Guide here](en/how-to/how-to-install-steam))
- 通过Steam安装了质子实验。
- 安装了软件包 `proton-run` (yay -S proton-run\`)。

## 用法

只需打开终端并运行：

```
proton-run /path/to/your/windows/program.exe
```

不会有很多应用正常工作。 有三个仿真器链来使这成为可能。
但是它是x86的仿真状态。