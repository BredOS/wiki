---
title: Orange Pi 6 Plus
description: 
published: true
date: 2025-12-22T07:21:41.440Z
tags: 
editor: markdown
dateCreated: 2025-11-24T07:14:51.932Z
---

[![sponsor-gold-tier-opi.png](/sponsors/sponsor-gold-tier-opi.png){.align-center}](http://www.orangepi.org)

# 1. Introduction
The Orange Pi 6 Plus is an ARM64 board with great specifications:
- SoC: CIX CD8160
- CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
- GPU: Immortals G720 MC10
- NPU: 28.8 Tops
- Network: 2x 5Gbit Ethernet (PCIe 4.0 1x lane each)

PCIe ports:
- 2x M.2 M key (PCIe 4.0 4x lanes)
- 1x M.2 E key (PCIe 4.0 2x lanes)

> We nicknamed it "*opi6plus*" or "*op6p*".
{.is-info}


# 2. Download
You can find download links for the aarch64 iso on our [Github page](https://github.com/BredOS/bredos-iso/releases/latest)!

Currently we offer one image based on the mainline kernel. This version does have missing drivers. A overview whats working on mainline and whats not can be found under [4. Mainline Support](#h-4-mainline-support).

# 3. Installation 

The opi6plus supports installation from generic ISO images, unlike our other supported single-board computers (SBCs) which use device-specific images. Installation can be done using a USB stick or even a USB optical drive. 
## 3.1 Generic ISO Installation 

A guide for generic .iso installation is available [here](/install/Installation-with-ISO). 


# 4. Mainline support
|   `linux`    | Status      |  Notes |
|--------------|-------------|--------|
| CPU          | Works    | |
| RAM          | Works    | |
| GPU          | Broken   | No driver|
| NPU          | Broken   | No driver|
| HW Encode    | Broken   | No driver|
| HW Decode    | Broken   | No driver|
| HDMI         | Partial  | EFI FB partially works (1080P@60Hz on most monitors) / 4K Monitors dont work while UEFI |
| DP           | Partial  | Woks fine |
| USB-C DP     | Partial  | No Output while UEFI |
| Storage      | Works    | M.2 SSDs work as expected |
| Ethernet     | Works    | |
| Front USB    | Works    | |
| Rear USB     | Works    | |
| Front audio  | Broken   | No driver|
| Rear audio   | Broken   | No driver|
| RTC          | Works    | No driver|
| UART         | Works    | `/dev/ttyS2` at boot|
| PCIe         | Works  | Works fine |
| M.2 E Key    | Works    | |
| M.2 M Key    | Works    | |
| Fan control  | Works    | Auto fan control, No way to control from OS |
