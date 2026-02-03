---
title: Install STEAM on BredOS (FEX-Emu)
description: 
published: false
date: 2026-02-03T09:17:38.531Z
tags: 
editor: markdown
dateCreated: 2026-01-27T09:08:49.245Z
---

# 1. Introduction

Welcome to the guide on how to install **Steam** on BredOS! Follow these simple steps to get Steam up and running on your system.

> This article is intended for SBCs based on an ARMv9 System-on-Chip, such as the Cix Pi 81x0. ARMv8 SoCs do support the execution of 32-bit code. For ARMv8 SBCs, use [box64](/en/how-to/how-to-install-steam) instead!
{.is-info}


# 2. Installation of FEX-Emu
## 2.1 Install FEX binary
As of the time of writing, you will need to compile FEX-Emu yourself. We have prepared a PKGBUILD file to simplify this process.

- Clone our FEX-Repo:
```
git clone https://github.com/BredOS/BredOS-FEX-Emu.git
```

- To build the latest release of FEX, you need to modify the PKGBUILD file:
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

- Go to https://github.com/FEX-Emu/FEX  and look for a valid tag. As of the time of writing, the latest release is from January 2026. The tag associated with this release is 2601. Edit the `pkgver` accordingly:

```
pkgver=2601
```

Close and Save with <kbd>CTRL</kbd> + <kbd>X</kbd>, then <kbd>Y</kbd>

- Build and install FEX with:
```
makepkg -si
```

## 2.2 Install x86_64 root filesystem
To simplify the installation of a BredOS x86_64 root filesystem, we developed our own `fex-config` tool. 

- To fetch the rootfs, run:
```
sudo fex-config -c
```

This will download and install BredOS to `~/.fex-emu/RootFS/bredos-chroot`



# 3. Installation of Steam
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
Intel and AMD graphics cards should work out of the box, provided that your host system has graphics acceleration enabled. 

> This has only been tested with AMD cards. If you have an Intel card, please feel free to share your experience over at our Discord or Telegram channel. 
{.is-warning}

## 4.2 NVidia
Ensure that you have installed the proprietary NVIDIA driver on your host system. The open-source Nouveau driver will not work. As long as our `fex-config` tool can detect the NVIDIA driver version, it will automatically install the x86_64 driver for you. 

> Refer to [here](https://github.com/MitchellAugustin/fex_autoinstall/blob/main/fex_autoinstall_poc.sh) for information on how the driver is installed.
{.is-info}


## 4.3 Any other GPU 
If you wish to use the internal graphics card of your Single Board Computer (SBC), you need to enable thunking. Thunk libraries serve as intermediaries that translate GPU calls. 

> Enabling thunks on FEX-Emu makes FEX extremely unstable!
{.is-warning}

- Edit the Config.json of FEX:
```
nano $HOME/.fex-emu/Config.json
```

- Locate the Thunks section of the configuration file:
```
  "ThunksDB": {
    "fex_thunk_test": 0,
    "asound": 0,
    "drm": 0,
    "Vulkan": 0,
    "WaylandClient": 0,
    "GL": 0
  }
```

- And edit it to enable `Vulkan`, `WaylandClient` and `GL`:
```
  "ThunksDB": {
    "fex_thunk_test": 0,
    "asound": 0,
    "drm": 0,
    "Vulkan": 1,
    "WaylandClient": 1,
    "GL": 1
  }
```

# 5. Launch Steam

- Once the installation is complete, you can launch Steam by searching for it in your application menu or by running:

```
steam
```

> Happy gaming!
{.is-success}

# 6. Troubleshooting
## 6.1 Steam hangs on start

- If Steam does not start for you, but hangs at:
```
steam.sh[7285]: Running Steam on bredos rolling 64-bit
steam.sh[7285]: STEAM_RUNTIME is enabled by the user
setup.sh[7328]: Steam runtime environment up-to-date!
```

- Open a new Console and execute:
```
killall FEXServer
```

Steam will then continue to load normally.

*[SBCs]: Single Board Computers
