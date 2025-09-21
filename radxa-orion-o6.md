---
title: Radxa Orion O6
description: 
published: true
date: 2025-09-21T10:44:09.419Z
tags: 
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. Introduction
The Orion O6 is an ITX-formatted ARM64 board with great specifications:
- SoC: CIX CD8180
- CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.6GHz + 4x A52 @ 1.8GHz
- GPU: Immortals G720 MC10
- NPU: 30 TOPs
- Network: 2x 5Gbit Ethernet (PCIe 4.0 1x lane each)

PCIe ports:
- M.2 M key (PCIe 4.0 4x lanes)
- M.2 E key (PCIe 4.0 2x lanes)
- Full sized PCIe x16 slot (PCIe 4.0 8x lanes)

> We nicknamed it "*Prion*" thanks to Panda's typing skills.
{.is-info}


# 2. Download
You can find download links for the aarch64 iso in our [Github page](https://github.com/BredOS/bredos-iso/releases/latest)!

We have two versions available: one is based on Radxa's 6.6 kernel, and the other is based on mainline. 
The version based on the 6.6 kernel has the name "ORION" attached and has support for the full feature set of that board. 
The mainline kernel does have missing drivers. A overview whats working on mainline and whats not can be found under [4. Mainline Support](#h-4-mainline-support).

# 3. Installation 

The Prion supports installation from generic ISO images, unlike our other supported single-board computers (SBCs) which use device-specific images. Installation can be done using a USB stick or even a USB optical drive. 
## 3.1 Generic ISO Installation 

A guide for generic .iso installation is available [here](/install/Installation-with-ISO). 
## 3.2 UEFI Installation 

We have developed a custom UEFI based on Radxa’s source code. It supports the actual CPU speed at which the board is sold, allows control of PCIe link speed, and – best of all – displays the Bred logo on startup. A full list of features and a guide for updating your UEFI is available [here](/radxa-orion-o6/prion-uefi-installation). 

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
| PCIe         | Partial  | Works fine for most devices but some GPUs don't work as expected. <br> Freezes the entire system sometimes. Consider using our bios.|
| M.2 E Key    | Works    | |
| M.2 M Key    | Works    | |
| Fan control  | Works    | Auto fan control, No way to control from OS |

# 5. PCIe
Some testers have found that the system becomes unstable when a device operating at PCIe Gen. 4 speeds is connected. If your board is unstable due to this, consider updating to our UEFI firmware and setting the link speed to Gen. 3.