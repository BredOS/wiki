---
title: Fix PCIe issues on Cix P1 SoCs
description: 
published: true
date: 2026-03-02T08:44:46.476Z
tags: 
editor: markdown
dateCreated: 2026-02-24T09:13:38.317Z
---

# 1. Intoduction

The Cix P1 81x0 SoCs firmware releases by different manufacturers have a bug in the SMMU v3 Event Queue, causing an interrupt storm that manifests as various problems. These range from missing features to crashing applications/desktops and kernel panics. [Eric Dedeoglu on GitHub conducted an in-depth analysis of this bug and found a fix for it](https://github.com/ErcinDedeoglu/orangepi-6plus-cix-sky1-smmu-fix). If you want to learn more about it, we highly recommend reading his article. 

# 2. The Fix
While Eric provides an install script on his GitHub, it only applies to Debian-based systems. Since Bred is based on ArchLinuxARM, we packaged the needed files for your convenience.

- Install `smmu-evtq-fix`
```
sudo pacman -Syu smmu-evtq-fix
```

> That's it. No reboot required (unless you have already limited your PCIe speed to Gen. 3 in the firmware. In that case, you will need to reboot your machine and revert this setting).
{.is-success}

# 3. Credits
Without Eric's analysis, this bug would not have been fixed. Thank you so much for your excellent work! 