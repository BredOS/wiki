---
title: Radxa Orion O6N
description: 
published: true
date: 2025-12-16T10:50:13.899Z
tags: 
editor: markdown
dateCreated: 2025-12-15T09:55:40.646Z
---

# 1. Introduction
The Orion O6 is an Nano ITX-formatted ARM64 board with great specifications:
- SoC: CIX CD8180
- CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.6GHz + 4x A52 @ 1.8GHz
- GPU: Immortals G720 MC10
- NPU: 30 TOPs
- Network: 2x 2.5Gbit Ethernet (PCIe 4.0 1x lane each)

PCIe ports:
- 2x M.2 M key (PCIe 4.0 4x lanes)
- M.2 E key (PCIe 4.0 2x lanes)
- M.2 B key (PCIe 4.0 2x lanes)

> We nicknamed it "*Fun Sized Prion*" because its like the [Prion](/en/radxa-orion-o6/prion), but fun sized.
{.is-info}


# 2. Download
You can find download links for the aarch64 iso on our [Github page](https://github.com/BredOS/bredos-iso/releases/latest)!

# 3. Installation 

The Fun Sized Prion supports installation from generic ISO images, unlike our other supported single-board computers (SBCs) which use device-specific images. Installation can be done using a USB stick or even a USB optical drive. 
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
| HDMI         | Partial  | EFI FB partially works (1080P@60Hz on most monitors) |
| DP           | Partial  | Same as above |
| USB-C DP     | Partial  | Same as above |
| Storage      | Works    | M.2 SSDs work as expected |
| Ethernet     | Works    | |
| Front USB    | Works    | Randomly dies, needs custom BredOS fork of Radxa bios to work|
| Rear USB     | Works    | Randomly dies|
| Front audio  | Broken   | No driver|
| Rear audio   | Broken   | No driver|
| RTC          | Works    | No driver|
| UART         | Works    | `/dev/ttyS2` at boot|
| PCIe (any M.2 Port)| Partial  | Works fine for most devices but some GPUs don't work as expected and freezes the entire system sometimes. See **5. PCIe** |
| M.2 E Key    | Works    | |
| M.2 M Key    | Works    | |
| M.2 B Key    | Works    | |
| Fan control  | Works    | Auto fan control, No way to control from OS |

# 5. PCIe
Some testers have found that the system becomes unstable when a device operating at PCIe Gen. 4 speeds is connected. If your board is unstable due to this, consider setting the link speed to Gen. 3.