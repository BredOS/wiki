---
title: BredOS News
description: Customizing this suprisingly complicated piece of software.
published: true
date: 2025-10-04T21:14:51.210Z
tags: 
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# Overview
BredOS News launches every time you open your shell.

BredOS by default configures `~/.bashrc` and `/etc/profile.d/99-bredos-news.sh` to run it by default.

Every copy of News is personalized.

You can fully configure which features of it you want, as well as theme it fully.

## Configuration & Overrides

BredOS News offers quite a few ways to customize it.
Permenant (per-user) configuration can be done at `~/.newsrc`.

The default blank configuration is automatically (re)generated after the first run of the app.
The default file looks like this at the time of writing:

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

`Accent` sets the primary colors, `Accent_Secondary` sets the colors for all the details.
Any arbitrary ANSI escape sequence may be applied.
For more info on ANSI escape sequences and examples, follow [this link](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).

### Disabling features
`Hush_Updates` removes the package updates section entirely.
`Hush_Disks` removes the attached medium storage usage notes.
`Hush_Smart` mutes disk failure warnings. This should NOT be used.

### Configuring animation time
`Time_Tick` configures the time between frames of the animation.
`Time_Refresh` configures how often the system details refresh.
These values are the best already. Do not reduce any further or cpu usage **will** spike.

`Onetime` disables the animation loop, the shortcut system and terminal resize functions.


## Shortcuts
`shortcuts` is a dictionary of settable keybinds. Quick-dial for your terminal.

While News is looping it's animation, pressing one of the configured keys will, instead of passing the key to the shell, launch the preconfigured shortcut. 

Setting keys, like how it's shown in the example, allows running commands or python functions.
Shell operations, like changing directory and/or piping are fully supported.
Special keys and combinations are currently not supported.
Symbols are supported.

## Environment overrides

Setting `HUSH_NEWS=1` will prevent BredOS News from running.

Creating `~/.hush_login` also has the same effect.