---
title: BredOS 新闻
description: 自定义这个非常复杂的软件。
published: true
date: 2025-10-06T07:18:15.049Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732 Z
---

# 2. 简介

默认情况下，"bredos-news" 每次打开外壳时都会触发。 默认情况下，"bredos-news" 每次打开外壳时都会触发。 这是由 `~/.bashrc` 中的 `bredos-news|| true` 行和`/etc/profile.d/99-bredos-news.sh` 行设置的。

每一个 ' bredos-news' 副本都可以个性化，这意味着你可以完全配置你想要的特征以及它的主题。

# 3. 配置和覆盖

BredOS 新闻提供了相当多的自定义方法。
Permenant (per user) 配置可以在 "~/.newsrc" 中完成。 一个permenant (每个用户) 配置可以设置为 "~/.newsrc"。 首次运行应用程序后自动生成默认空白配置(重新)， 这样可以通过删除此文件来重置它的配置。

- 默认配置文件看起来像这样：

```
"""
BredOS-News Configuration

Refer to `https://wiki.bredos.org/customizations/news`,
for detailed instructions on how to configure.
"""

# Accent = "\033[38;5;129m"
# Accent_Secondary = "\033[38;5;104m"

# Hush_Updates = False
# Hush_Disks = False
# Hush_Smart = False
# Time_Tick = 0.1
# Time_Refresh = 0.25
# Onetime = False

"""
Shortcuts configuration

Shell commands, using $SHELL, and python functions are fully supported.
Only alphanumeric and symbol keys can be captured, no key combinations.
Capital keys work and can be bound to seperate shortcuts from lowercase.
"""

def shortcuts_help() -> None:
    print("Configured shortcuts:")
    for i in shortcuts.keys():
        shortcut = shortcuts[i]
        if is_function(shortcut):
            print(f" - {i}: Function {shortcut.__name__}")
        else:
            print(f' - {i}: "{shortcuts[i]}"')
    print("\n")

shortcuts["1"] = "bredos-config"
shortcuts["0"] = "sudo sys-report"
shortcuts["?"] = shortcuts_help
```

> 要激活此配置文件中的参数，请在行开始处删除 <kbd>#</kbd>。
> {.is-info}
> {.is-info}

## 2.1 设置音量(颜色)

参数`Accent` 设置了主颜色，`Accent_Secondary` 为所有细节设置颜色。 任何武断的 ANSI 逃脱序列都可以应用。 任何武断的 ANSI 逃脱序列都可以应用。

> 关于ANSI逃避序列和示例的更多信息，请点击[此链接](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797)。
> {.is-info}
> {.is-info}

常用样式：

| 颜色    | 代码                                                                                        |
| ----- | ----------------------------------------------------------------------------------------- |
| 完美的紫色 | \\`Accent = "\033[38;5;129m""                                  |
|       | \\`Accent_Second = "\033[38;5;104m""      |
| 粗体    | \\`Accent = "\033[1m\033[38;5;124m"" |
|       | \\`Accent_Second = "\033[38;5;160m""      |

## 禁用功能

| 参数                       | 简介                   |
| ------------------------ | -------------------- |
| `Hush_Updates` = `False` | 完全删除软件包更新部分。         |
| `Hush_Disks` = `False`   | 移除附加的媒体存储使用说明。       |
| `Hush_Smart` = `False`   | 静音磁盘失败警告。 应该使用**不**。 |

## 配置动画时间

| 参数                      | 快捷键                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------- |
| `Time_Tick` = `0.1`     | `Time_Tick`配置动画帧之间的时间。&#xA;`Time_Refresh` 配置系统详细信息刷新的频率。&#xA;这些值已经是最好的。 不要再减少任何cpu的使用 \*\*will \*\* 溢出。 |
| `Time_Refresh` = `0.25` | 配置系统细节刷新频率。                                                                                             |
| `Onetime` = `False`     | `Onetime` 禁用动画循环、快捷方式系统和终端调整大小函数。                                                                       |

> 这些值已经是最好的。 不要再减少任何cpu的使用 \*\*will \*\* 溢出。
> {.is-info}

# 4. 快捷键

`shortcuts` 是一个可设置键绑定的字典。 快速拨打您的终端。 这基本上是快速拨打您的终端。 "快捷键" 数组是一个可设置键绑定的字典。 这基本上是快速拨打您的终端。 虽然`bredos-news`是循环它的动画，但按下一个配置的密钥将不会将该密钥传递给外壳，而是启动预配置的快捷方式。

设置快捷键，如在示例中的显示方式，允许运行命令或python函数。 对于上面给出的示例，按下 <kbd>1</kbd> 将会启动工具“bredos-config”。 设置键像它在示例中显示的那样，允许运行命令或python函数。
完全支持 Shell 操作，如更改目录和/或管道。
当前不支持特殊键和组合。
支持符号。

# 🚀 4. 环境覆盖

设置 `HUSH_NEWS=1` 将阻止BredOS 新闻运行。
