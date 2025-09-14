---
title: Proton-run
description: Quick explainer on using the BredOS `proton-run` script
published: true
date: 2025-09-13T09:47:37.755Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# Using proton-run to run windows apps

The tool `proton-run` is a recently released package that allows you to use Steam's Proton Experimental to run x86_64 Windows applications under BredOS ARM64.

## 1. Requirements

- An RK3588 system running BredOS.
- Steam. ([Guide here](/how-to/how-to-install-steam))

## 2. 安裝

### 2.1 Install Steam's Proton Experimental

Open Steam and navigate to your `Library`. Click into the searchbar and type `proton`. Choose `Proton Experimental` and install it. Other versions of proton will not work.

### 2.2 Install proton-run

Install `proton-run` with the command

```
yay -S proton-run
```

## 3. Usage

Simply open a terminal and run:

```
proton-run /path/to/your/windows/program.exe
```

> Not a lot of apps will work. There are three emulators chainloaded to make this possible.
> But it's the state of x86 emulation.
> {.is-warning}
