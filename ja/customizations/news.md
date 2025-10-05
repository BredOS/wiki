---
title: BredOS ニュース
description: この驚くほど複雑なソフトウェアをカスタマイズします
published: true
date: 2025-10-05T06:49:33.972Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🔄 1. はじめに

デフォルトでは、シェルを開くたびに「bredos-news」が起動します。 `~/.bashrc` と `/etc/profile.d/99-bredos-news.sh` の設定で設定します。

「bredos-news」のすべてのコピーをパーソナライズすることができます。つまり、あなたが望む機能とそれを完全にテーマに設定することができます。

# 3. 設定と上書き

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
> {.is-warning}

## 2.1 Set accent (color)

The parameter `Accent` sets the primary colors, `Accent_Secondary` sets the colors for all the details. 任意の ANSI エスケープシーケンスを適用することができます。

> ANSI エスケープシーケンスと例の詳細については、[this link](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797) に従ってください。
> {.is-warning}

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

> これらの値はすでに最高です。 これ以上もしくはcpuの使用を減らさないでください **スパイク** 。
> {.is-warning}

# 4. ショートカット

The `shortcuts` array is a dictionary of settable keybinds. This is basically quick-dial for your terminal. While `bredos-news` is looping it's animation, pressing one of the configured keys will, instead of passing the key to the shell, launch the preconfigured shortcut.

Setting shortcut keys, like how it's shown in the example, allows running commands or python functions. For the given example above, pressing <kbd>1</kbd> will launch the tool `bredos-config`. All shell operations, like changing directory and/or piping, are fully supported, while special keys and key combinations are currently not supported.

# 4. 環境の上書き

Setting the variable `HUSH_NEWS=1` or creating the file `~/.hush_login` will prevent BredOS News from running.
