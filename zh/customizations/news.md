---
title: BredOS 新闻
description: 自定义这个非常复杂的软件。
published: true
date: 2025-10-05T06:49:33.972Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732 Z
---

# 2. 简介

默认情况下，"bredos-news" 每次打开外壳时都会触发。 这是由`~/.bashrc`和`/etc/profile.d/99-bredos-news.sh`中的配置设置的。

每一个 ' bredos-news' 副本都可以个性化，这意味着你可以完全配置你想要的特征以及它的主题。

# 3. 配置和覆盖

A permenant (per-user) configuration can be set at `~/.newsrc`. A default blank configuration is automatically (re)generated after the first run of the app, so it is possible to reset its configuration by deleting this file.

- The default configuration file should look like this:

```
# BredOS-News Configuration

# Accent = "\033[38;5;129m"
# Accent_Secondary = "\033[38;5;104m"

# Hush_Updates = False
# Hush_Disks = False
# Hush_Smart = False
# Time_Tick = 0.1
# Time_Refresh = 0.25
# Onetime = False

# Shortcuts configuration

# shortcuts = {
#     "1": "bredos-config",
# }
```

> To activate a parameter in this configuration file, remove the <kbd>#</kbd> at the beginning of the line.
> {.is-info}

## 2.1 Set accent (color)

The parameter `Accent` sets the primary colors, `Accent_Secondary` sets the colors for all the details. 任何武断的 ANSI 逃脱序列都可以应用。

> 关于ANSI逃避序列和示例的更多信息，请点击[此链接](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797)。
> {.is-info}

## 2.2 Disabling features

| Parameter                | Description                                                                               |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| `Hush_Updates` = `False` | Removes the package updates section entirely.                             |
| `Hush_Disks` = `False`   | Removes the attached medium storage usage notes.                          |
| `Hush_Smart` = `False`   | Mutes disk failure warnings. This should **not** be used. |

## 2.3 Configuring animation time

| Parameter               | Description                                                                                     |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| `Time_Tick` = `0.1`     | Configures the time between frames of the animation.                            |
| `Time_Refresh` = `0.25` | Configures how often the system details refresh.                                |
| `Onetime` = `False`     | Disables the animation loop, the shortcut system and terminal resize functions. |

> 这些值已经是最好的。 不要再减少任何cpu的使用 \*\*will \*\* 溢出。
> {.is-info}

# 4. 快捷键

The `shortcuts` array is a dictionary of settable keybinds. This is basically quick-dial for your terminal. While `bredos-news` is looping it's animation, pressing one of the configured keys will, instead of passing the key to the shell, launch the preconfigured shortcut.

Setting shortcut keys, like how it's shown in the example, allows running commands or python functions. For the given example above, pressing <kbd>1</kbd> will launch the tool `bredos-config`. All shell operations, like changing directory and/or piping, are fully supported, while special keys and key combinations are currently not supported.

# 🚀 4. 环境覆盖

Setting the variable `HUSH_NEWS=1` or creating the file `~/.hush_login` will prevent BredOS News from running.
