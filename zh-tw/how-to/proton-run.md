---
title: Proton-run
description: Quick explainer on using the BredOS `proton-run` script
published: true
date: 2025-09-15T09:55:16.279Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# 1. 簡介

The tool `proton-run` is a recently released package that allows you to use Steam's Proton Experimental to run x86_64 Windows applications under BredOS ARM64.

# 2. Requirements

- An RK3588 system running BredOS.
- Steam. ([Guide here](/how-to/how-to-install-steam))

# 3. 安裝

## 3.1 Install Steam's Proton Experimental

Open Steam and navigate to your `Library`. Click into the searchbar and type `proton`. Choose `Proton Experimental` and install it.

> Other versions of proton will not work.
> {.is-info}

## 3.2 Install proton-run

- Install `proton-run` with the command

```
yay -S proton-run
```

# 4. Usage

- Simply open a terminal and run:

```
proton-run /path/to/your/windows/program.exe
```

> Not a lot of apps will work. There are three emulators chainloaded to make this possible.
> But it's the state of x86 emulation.
> {.is-warning}
