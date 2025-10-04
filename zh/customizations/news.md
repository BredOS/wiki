---
title: BredOS 新闻
description: 自定义这个非常复杂的软件。
published: true
date: 2025-10-04T21：14：51.210Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732 Z
---

# 简介

BredOS 新闻每次打开您的外壳时都会触发。

默认情况下，BredOS 配置`~/.bashrc`和`/etc/profile.d/99-bredos-news.sh`来运行它。

每份新闻都是个性化的。

您可以充分配置您想要的功能以及主题。

## 配置和覆盖

BredOS 新闻提供了相当多的自定义方法。
Permenant (per user) 配置可以在 "~/.newsrc" 中完成。

首次运行后自动生成默认空白配置。
在写入时默认文件看起来就像这样：

```
# BredOS-News Configuration

# Accent = "\033[38;5;129m"
# Accent_Second= "\033[38;5; 04m"

# Hush_Updates = False
# Hush_Disks = False
# Hush_Smart = False
# Time_Tick = 0.
# 时间刷新= 0。 5
# 1time = False

# 快捷键配置

# 快捷键= Power
# "1": "bredos-config",
# }
```

`Accent` 设置主颜色，`Accent_Secary` 为所有细节设置颜色。
任何武断的 ANSI 逃脱序列都可以应用。
关于ANSI逃避序列和示例的更多信息，请点击[此链接](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797)。

### 禁用功能

`Hush_Updates` 完全删除软件包更新部分。
`Hush_Disks`删除附加的介质存储使用说明。
`Hush_Smart` 静音磁盘失败警告。 不应使用这种方法。

### 配置动画时间

`Time_Tick`配置动画帧之间的时间。
`Time_Refresh` 配置系统详细信息刷新的频率。
这些值已经是最好的。 不要再减少任何cpu的使用 \*\*will \*\* 溢出。

`Onetime` 禁用动画循环、快捷方式系统和终端调整大小函数。

## 快捷键

`shortcuts` 是一个可设置键绑定的字典。 快速拨打您的终端。

当新闻正在循环它的动画时，按一种已配置的密钥将不会将密钥传递给外壳，而是启动预配置的快捷方式。

设置键像它在示例中显示的那样，允许运行命令或python函数。
完全支持 Shell 操作，如更改目录和/或管道。
当前不支持特殊键和组合。
支持符号。

## 环境覆盖

设置 `HUSH_NEWS=1` 将阻止BredOS 新闻运行。

创建 "~/.hush_login" 也具有同样的效果。