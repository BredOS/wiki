---
title: BredOS News
description: Customizing this suprisingly complicated piece of software.
published: true
date: 2025-10-05T12:26:26.876Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🎛️ 1. 簡介

BredOS News launches every time you open your shell. This is set by a configuration in `~/.bashrc` and `/etc/profile.d/99-bredos-news.sh`.

Every copy of `bredos-news` can be personalized, which means you can fully configure which features of it you want, as well as theme it fully.

# 3. Configuration & Overrides

Permenant (per-user) configuration can be done at `~/.newsrc`. The default blank configuration is automatically (re)generated after the first run of the app.

- The default file looks like this at the time of writing:

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

`Accent` sets the primary colors, `Accent_Secondary` sets the colors for all the details. Any arbitrary ANSI escape sequence may be applied.

> For more info on ANSI escape sequences and examples, follow [this link](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).
> {.is-info}

Common styles:

| Color          | Code                                   |
| -------------- | -------------------------------------- |
| Perfect Purple | `Accent = "\033[38;5;129m"`           |
|                | `Accent_Secondary = "\033[38;5;104m"` |
| Bold Red       | `Accent = "\033[1m\033[38;5;124m"`   |
|                | `Accent_Secondary = "\033[38;5;160m"` |

## Disabling features

| Parameter                | Shortcuts                                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------- |
| `Hush_Updates` = `False` | `Hush_Updates` removes the package updates section entirely.                       |
| `Hush_Disks` = `False`   | `Hush_Disks` removes the attached medium storage usage notes.                      |
| `Hush_Smart` = `False`   | `Hush_Smart` mutes disk failure warnings. This should NOT be used. |

## Configuration & Overrides

| Parameter               | 簡介                                                                                                        |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| `Time_Tick` = `0.1`     | Configuring animation time                                                                                |
| `Time_Refresh` = `0.25` | `Time_Refresh` configures how often the system details refresh.                           |
| `Onetime` = `False`     | `Onetime` disables the animation loop, the shortcut system and terminal resize functions. |

> These values are the best already. Do not reduce any further or cpu usage **will** spike.
> {.is-info}

# 4. Shortcuts

`shortcuts` is a dictionary of settable keybinds. Quick-dial for your terminal. While News is looping it's animation, pressing one of the configured keys will, instead of passing the key to the shell, launch the preconfigured shortcut.

Setting keys, like how it's shown in the example, allows running commands or python functions. For the given example above, pressing <kbd>1</kbd> will launch the tool `bredos-config`. Shell operations, like changing directory and/or piping are fully supported. Special keys and combinations are currently not supported.

# 🔁 4. Environment overrides

Setting `HUSH_NEWS=1` will prevent BredOS News from running.
