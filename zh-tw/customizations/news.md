---
title: BredOS News
description: Customizing this suprisingly complicated piece of software.
published: true
date: 2025-10-05T13:04:29.052Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🎛️ 1. 簡介

By default `bredos-news` launches every time you open your shell. This is set by the line `bredos-news || true` in `~/.bashrc` and by the existence of `/etc/profile.d/99-bredos-news.sh`

Every copy of `bredos-news` is personalized, which means you can fully configure which features of it you want, as well as theme it fully.

# 3. Configuration & Overrides

A permenant (per-user) configuration can be set at `~/.newsrc`. A default blank configuration is automatically (re)generated after the first run of the app, so it is possible to reset its configuration by deleting this file.

- The default configuration file should look like this:

```
"""
BredOS-News Configuration

Refer to `https://wiki.bredos.org/e/en/customizations/news`,
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

> To activate a parameter in this configuration file, remove the <kbd>#</kbd> at the beginning of the line.
> {.is-info}

## 2.1 Set accent (color)

The parameter `Accent` sets the primary colors, `Accent_Secondary` sets the colors for all the details. Any arbitrary ANSI escape sequence may be applied.

> For more info on ANSI escape sequences and examples, follow [this link](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).
> {.is-info}

Common styles:

| Color          | Code                                   |
| -------------- | -------------------------------------- |
| Perfect Purple | `Accent = "\033[38;5;129m"`           |
|                | `Accent_Secondary = "\033[38;5;104m"` |
| Bold Red       | `Accent = "\033[1m\033[38;5;124m"`   |
|                | `Accent_Secondary = "\033[38;5;160m"` |

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

> These values are the best already. Do not reduce any further or cpu usage **will** spike.
> {.is-info}

# 4. Shortcuts

The `shortcuts` array is a dictionary of settable keybinds. This is basically quick-dial for your terminal. While `bredos-news` is looping it's animation, pressing one of the configured keys will, instead of passing the key to the shell, launch the preconfigured shortcut.

Setting shortcut keys, like how it's shown in the example, allows running commands or python functions. For the given example above, pressing <kbd>1</kbd> will launch the tool `bredos-config`. All shell operations, like changing directory and/or piping, are fully supported, while special keys and key combinations are currently not supported.

# 🔁 4. Environment overrides

Setting the variable `HUSH_NEWS=1` or creating the file `~/.hush_login` will prevent BredOS News from running.
