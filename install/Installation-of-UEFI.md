---
title: Installation of UEFI
description: 
published: false
date: 2025-09-16T11:45:20.692Z
tags: 
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. Introduction
Many of our supported devices do offer support for `UEFI`, which is a modern firmware interface that initializes hardware and starts the operating system. With the help of `UEFI` your device is capable of booting .iso files (written to a USB-Stick or burned to a DVD) as well as booting your OS directly from the nVME drive or over the network via PXE.

# 2. Examine your device
Sadly, not all devices we support do support booting `UEFI`. Also, not every device does come with an SPI chip installed. 
If you have a device that supports `UEFI` and has a SPI chip, follow `3.1 Installation to SPI`. 
If your device does support but has no SPI chip follow `3.2 Installation to SD Card`.

- To determine what your device is capable of check [this table](/en/table-of-supported-devices).

# 3. Installation
## 3.1 Installation to SPI

## 3.2 Installation to SD Card