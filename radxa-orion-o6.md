---
title: Radxa Orion O6
description: 
published: false
date: 2025-09-17T08:50:00.224Z
tags: 
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. Introduction
The Radxa Orion O6 is a Mini‑ITX motherboard powered by the Cix P1 (CD8180) SoC, featuring a 12‑core ARM v9.2 CPU with 4 big Cortex‑A720 cores (~2.8 GHz), 4 medium A720s (~2.4 GHz), and 4 little Cortex‑A520s (~1.8 GHz).  It includes an Arm Immortalis‑G720 GPU and a 30 TOPS NPU for AI inference.  With up to 64 GB LPDDR5, multiple display outputs, dual 5 GbE networking, and PCIe Gen 4 expansion, it’s aimed at edge AI, multimedia, and developer workstation applications.

> We nicknamed it "*Prion*" thanks to Pandas typing skills.
{.is-info}


# 2. Download
You can find download links for the aarch64 iso in our [Github page](https://github.com/BredOS/bredos-iso/releases/latest)!

We have two versions available: one is based on Radxa's 6.6 kernel, and the other is based on mainline. The version based on the 6.6 kernel has the name "ORION" attached and has support for the full feature set of that board. The mainline kernel does have missing drivers. A good overview whats working on mainline and whats not can be found [here](/en/table-of-supported-devices).

# 3. Installation 

The Prion supports installation from generic ISO images, unlike our other supported single-board computers (SBCs) which use device-specific images. Installation can be done using a USB stick or even a USB optical drive. 
## 3.1 Generic ISO Installation 

A guide for generic .iso installation is available here. 
## 3.2 UEFI Installation 

We have developed a custom UEFI based on Radxa’s source code. It supports the actual CPU speed at which the board is sold, allows control of PCIe link speed, and – best of all – displays the Bred logo on startup. A guide for updating your UEFI is available [here](/en/radxa-orion-o6/prion-uefi-installation). 

# 4. PCIe
Some testers have found that the system becomes unstable when a device operating at PCIe Gen. 4 speeds is connected. If your board is unstable due to this, consider updating to our UEFI firmware and setting the link speed to Gen. 3.