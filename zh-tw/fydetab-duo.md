---
title: Fydetab Duo
description: null
published: true
date: 2024-11-10T19:45:29.939Z
tags: null
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# Fydetab Duo

The device has and supports Cinnamon and KDE, but workarounds to working with gnome are also available.

# 安裝

Briefly, we use `rkdeveloptool` to flash the image to the eMMC. Commands are as follows:

```bash
# first, put the device in maskrom mode
# and flash the spi loader
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# then flash the os image
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

For detailed instructions, refer to [📦 How to install to eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)

# Guides

- [🐾 How to setup Panthor on Mali GPUs with RK3588](/en/how-to/how-to-setup-panthor)
- [🎮  How to Install STEAM on BredOS](/en/how-to/how-to-install-steam)
- [🦶  GNOME on the Fydetab](/fydetab-duo/gnome)
- [📦 How to install to eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [🔧 More Info in fydetabduo wiki](https://wiki.fydetabduo.com/category/-bredos)
