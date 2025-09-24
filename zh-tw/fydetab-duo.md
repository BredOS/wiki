---
title: Fydetab Duo
description:
published: true
date: 2025-09-17T10:16:17.074Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# 1. 簡介

The Fydetab Duo is a 2‑in‑1 tablet developed by Fyde Innovations, makers of FydeOS — a Chromium‑OS based system (Linux‑derived) which can also run Android apps. It’s designed to be usable as a tablet or with a detachable keyboard/case + stylus to function more like a small laptop.

Key specifications:

- Display: 12.35″ IPS panel, resolution ~ 2560×1600, brightness ~ 500 nits.
- Processor: ARM‑based Rockchip RK3588S SoC.
- Memory & storage: 8 GB LPDDR4X RAM; storage is 128 GB eMMC. Expandable via microSD.
- Battery: ≈ 42 Wh, estimated battery life up to ~10 hours.
- Other features: Wi‑Fi 6, Bluetooth 4.2, fingerprint sensor, stereo speakers, 5 MP front camera, stylus support.

> We nicknamed it "_FydeTube_", "_FDT_", or "_Duo_", take your pick.
> {.is-info}

# 2. Download

You can find download links for images in our [website](https://bredos.org/download.html)!

# 3. 安裝

- Briefly, we use `rkdeveloptool` to flash the image to the eMMC. Commands are as follows:

```bash
# first, put the device in maskrom mode
# and flash the spi loader
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# then flash the os image
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

For detailed instructions, refer to [📦 How to install to eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)

# 4. Useful links

- [🐾 How to setup Panthor on Mali GPUs with RK3588]/how-to/how-to-setup-panthor)
- [🎮  How to Install STEAM on BredOS]/how-to/how-to-install-steam)
- [Switch Desktop Environment](/en/how-to/switch-desktop-environments)
- [📦 How to install to eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [🔧 More Info in fydetabduo wiki](https://wiki.fydetabduo.com/category/-bredos)
