---
title: Radxa Orion O6
description: 
published: false
date: 2025-09-17T06:04:34.142Z
tags: 
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. Introduction
The Radxa Orion O6 is a Mini‑ITX motherboard powered by the Cix P1 (CD8180) SoC, featuring a 12‑core ARM v9.2 CPU with 4 big Cortex‑A720 cores (~2.8 GHz), 4 medium A720s (~2.4 GHz), and 4 little Cortex‑A520s (~1.8 GHz).  It includes an Arm Immortalis‑G720 GPU and a 30 TOPS NPU for AI inference.  With up to 64 GB LPDDR5, multiple display outputs, dual 5 GbE networking, and PCIe Gen 4 expansion, it’s aimed at edge AI, multimedia, and developer workstation applications.

> We nicknamed it "*Prion*" thanks to Pandas typing skills.
{.is-info}


# 2. Download
You can find download links for the aarch64 iso in our [github page](https://github.com/BredOS/bredos-iso/releases/latest)!

# 3. Installation

The Prion supports installation from generic ISO images, in contrast to our other supported SBCs which use device-specific images. Installation can be done from a USB stick or even a USB optical drive.

## 3.1 Generic ISO Installation

A guide for installation can be found here.

## 3.2 UEFI Installation

We developed a custom UEFI based on Radxa’s source code. It supports the actual CPU speed the board is sold with, allows control of PCIe link speed, and – best of all – displays the Bred logo on startup. A guide for updating your UEFI can be found here.