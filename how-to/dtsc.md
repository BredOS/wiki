---
title: Using DTSC
description: Using the BredOS Device Tree Source Compiler helper script
published: true
date: 2025-05-07T13:18:58.737Z
tags: 
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# DTSC

`dtsc` is a command shipped by default along with BredOS along with the `bredos-tools` package.
For it to function however you need to install `dtc`, simply run `yay -S dtc`

The script is a wrapper to dtsc, performing automatic gcc preprocessing, linking and generation of needed files.
It makes generation and testing of device trees a lot simplier.
It automatically determines and generates base device trees or overlays accordingly.

## IMPORTANT NOTE
**Installing an incorrect device tree on your device will render it inoperable.**
**Be careful, perform backups and ensure a contigency plan.**