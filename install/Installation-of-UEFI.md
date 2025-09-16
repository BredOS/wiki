---
title: Installation of UEFI
description: 
published: false
date: 2025-09-16T11:29:43.061Z
tags: 
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. Introduction
Many RK35xx-based devices do offer support for `UEFI`, which is a modern firmware interface that initializes hardware and starts the operating system. With the help of `UEFI` your device is capable of booting .iso files (written to a USB-Stick or burned to a DVD) as well as booting your OS directly from the nVME drive.

# 2. Examine your device
Sadly, not all devices we support do support booting `UEFI`. Also, not every device does come with an SPI chip installed. If you have a device that supports `UEFI` and has a SPI chip, follow `3.1 Installtion to SPI`. If your device does support but has no SPI chip follow `3.2 Installation to SD Card`.

- To determine what your device is capable of check this table:

| Device            | UEFI  | SPI Chip | Known Issues |
|-------------------|-------|-----------|--------------|
| Cool Pi 4 Model B       |  No   |         | |
|FydeTab Duo|	|	|	|
|Indiedroid Nova|	|	|	|
|ITX-3588J|	Yes |	No |	|
|Khadas Edge 2|	|	|	|
|Khadas VIM 4|	|	|	|
|Mekotronics R58S|	|	|	|
|Mekotronics R58X|	|	|	|
|Mekotronics R58X-4G|	|	|	|
|Mekotronics R58X-Pro|	|	|	|
|Milk V Jupiter|	|	|	|
|Orange Pi 5|	|	|	|
|Orange Pi 5 Max|	|	|	|
|Orange Pi 5 Plus|	Yes |	|	|
|Orange Pi 5 Pro|	|	|	|
|Orange Pi 5 Ultra|	|	|	|
|Orange Pi CM5|	|	|	|
|Orange Pi RV2|	|	|	|
|Radxa CM5|	|	|	|
|Radxa CM5 DTV carrier|	|	|	|
|Radxa NX5 Kit|	|	|	|
|Radxa Rock 4C Plus|	|	|	|
|Radxa Rock 5 ITX|	|	|	|
|Radxa Rock 5A|	|	|	|
|Radxa Rock 5B|	|	|	|
|Radxa Rock 5B+|	|	|	|
|Radxa Rock 5C|	|	|	|
|Radxa Rock 5D|	|	|	|
|Radxa Rock 5T|	|	|	|