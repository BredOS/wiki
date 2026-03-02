---
title: 在 Cix P1 SoC 修复PCI问题
description:
published: true
date: 2026-03-02T08:44.476Z
tags:
editor: markdown
dateCreated: 2026-02-24T09:13:38.317Z
---

# 2. 上岗培训

不同制造商发布的 Cix P1 81x0 SOC固件在SMMU v3 事件队列中有一个错误， 造成一场打断风暴，表现为各种问题。 这些功能从缺失的功能到崩溃应用程序/桌面和内核恐慌。 [GitHub 上的Eric Dedeoglu对此错误进行了深入分析并找到了一个解决方案](https://github.com/ErcinDedeoglu/orangepi-6plus-cix-sky1-smmu-fix)。 如果您想了解更多信息，我们强烈建议阅读他的文章。

# 1. 修复

虽然Eric 在他的GitHub 上提供一个安装脚本，但它只适用于基于 Debian的系统。 因为Bred 基于 ArchLinuxARM ，我们打包了所需的文件以方便您。

- 安装 `smmu-evtq-fix`

```
sudo pacman -Syu smmu-evtq-fix
```

> 就是这样。 无需重启(除非您已经将您的 PCIe 速度限制为 3 级固件)。 在这种情况下，您需要重新启动您的机器并恢复此设置)。
> 快乐游戏！
> {.is-success}
> {.is-success}

# 🔁 3. 致谢

没有Eric的分析，这个错误本来不会被修复。 非常感谢您的出色工作！