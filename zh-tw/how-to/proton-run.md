---
title: Proton-run
description: Quick explainer on using the BredOS `proton-run` script
published: true
date: 2025-05-07T14:44:47.710Z
tags: null
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# Using `proton-run`

`proton-run` is a recently released package that allows you to use Steam's Proton Experimental to run x86_64 Windows applications under BredOS ARM64.

## Requirements

- An RK3588 system running BredOS.
- Steam. ([Guide here](en/how-to/how-to-install-steam))
- Having installed Proton Experimental through Steam.
- Having installed the package `proton-run` (`yay -S proton-run`).

## Usage

Simply open a terminal and run:

```
proton-run /path/to/your/windows/program.exe
```

Not a lot of apps will work. There are three emulators chainloaded to make this possible.
But it's the state of x86 emulation.