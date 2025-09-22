---
title: BredOS 配置
description:
published: false
date: 2025-09-21T09:27:32.905Z
tags:
editor: markdown
dateCreated: 2025-09-21T09:27:04.136Z
---

# 1. 简介

- 开发了“bredos-config”工具来简化系统的更改、维护和管理。

![main.png](/bredos-config/main.png)

> 默认情况下，工具“bredos-config”已安装。
> {.is-info}
> {.is-info}

- 如果您删除了它或想要重新安装它，请运行：

```
sudo pacman -S bredos-config
```

# 2. 功能

## 2.1 设备树管理器

- 此选项可帮助您管理设备树和设备树叠加层，用于更改内核与设备的相互作用。 一个简单的例子是使用 Orange Pi 5 Plus 禁用LED，但还有更多的东西要探索。 Follow [this article](/how-to/how-to-enable-dtbos) to learn more about it. 一个简单的例子是使用 Orange Pi 5 Plus 禁用LED，但还有更多的东西要探索。 Follow [this article](/how-to/how-to-enable-dtbos) to learn more about it.

![dtb-manager.png](/bredos-config/dtb-manager.png)

## 2.2 更新系统

> 此选项正在构建中！
> {.is-warning}
> {.is-warning}

## 2.3 系统升级

- 在本节中， 您会找到一些有用的任务来保持系统清理并顺利运行，如执行文件系统维护任务或检查系统的完整性。

![upkeep.png](/bredos-config/upkeep.png)

## 2.4 系统调整

- 在这里您可以找到一些有用的调整方法来适应您的系统：

![tweaks.png](/bredos-config/tweaks.png)

## 2.5 迁移

> 为什么这合并到系统调整？
> {.is-danger}
> {.is-danger}

## 2.6 包

- 在这里，你会找到各种钩子来帮助你安装很酷的东西，如蒸汽或码头：

![packages.png](/bredos-config/packages.png)