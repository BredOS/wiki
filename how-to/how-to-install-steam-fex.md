---
title: Install Steam on BredOS (FEX-Emu)
description: 
published: false
date: 2026-01-27T09:08:49.245Z
tags: 
editor: markdown
dateCreated: 2026-01-27T09:08:49.245Z
---

# 1. Introduction

Welcome to the guide on how to install **Steam** on BredOS! Follow these simple steps to get Steam up and running on your system.

> This article is intended for Single Board Computers (SBCs) based on an ARMv9 System-on-Chip (SoC), such as the Cix Pi 8080. ARMv8 SoCs do support the execution of 32-bit code. For ARMv8 SBCs, use box64 instead!
{.is-info}


# 2. Installatoin of FEX-Emu
## 2.1 Install FEX binary
As of the time of writing you need to compile FEX-Emu by yourself. We prepared a PKGBUILD file to simplify things.

- Clone our FEX-Repo:
```
git clone https://github.com/BredOS/BredOS-FEX-Emu.git
```

- To build the lastest release of FEX you need to alter the PKGBUILD file:
```
cd BredOS-FEX-Emu/BredOS
nano PKGBUILD
```

- The file should look like this:
```
pkgname=bredos-fex-emu
pkgver=2509.1
pkgrel=2
pkgdesc='Fast usermode x86 and x86-64 emulator for Arm64 - BredOS Edition'
url=https://BredOS.org
arch=(aarch64)
license=(GPL3)

[and so on ...]
```

- Go to https://github.com/FEX-Emu/FEX and look up a valid tag. As of the time of writeing the latest release is from Januar of 2026. The Tag attached to this is 2601. Edit the `pkgver` accordingly:

```
pkgver=2601
```

Close and Save with <kbd>CTRL</kbd> + <kbd>X</kbd>, then <kbd>Y</kbd>

- Build and install FEX with:
```
makepkg -si
```

## 2.2 Install x86_64 root filesystem
To make the installation of a BredOS x86_64 root filesystem easier, why developed our own fex-config tool.

- To fetch the rootfs, run:
```
sudo fex-config -c
```

This will download and install BredOS to `~/.fex-emu/RootFS/bredos-chroot`



# 3. Installation Steam
## 3.1 Enable multilib
You may need to add the **BredOS Multilib** repository to install Steam and the necessary translation layers. To do this, follow these steps:

- Install `bredos-multilib` package
```
   sudo pacman -S bredos-multilib
```

- Update the package database by running:

```
   sudo pacman -Sy
```

## 3.2 Steam Installation


- Run the following command to install Steam:

```
   sudo pacman -Sdd steam
```

# 4. GPU Acceleration
## 4.1 Intel and AMD
Intel and AMD Graphics Card should work out of the box as long as your hostsystem has graphics accerleration enabled.

> This is only tested for AMD. Feel free to share your experience if you have an Intel Card
{.is-warning}

## 4.2 NVidia
Make sure you have installed the NVidia driver on your hostsystem. The open source nouveau driver does not work.



# 5. Launch Steam

- Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:

```
steam
```

> Happy gaming!
{.is-success}

