---
title: Radxa Orion Series
description:
published: false
date: 2025-09-17T00:28:55.869Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:08:50.283Z
---

# 簡介

SoC: CIX CD8180
CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
GPU: Immortals G720 MC10
NPU: 30 TOPs
Network: 2x 5Gbit Ethernet (PCIe 4.0 1x lane each)
PCIe:

- M.2 M key (PCIe 4.0 4x lanes)
- M.2 E key (PCIe 4.0 2x lanes)
- Full sized PCIe x16 slot (PCIe 4.0 8x lanes)

# Mainline support

| `linux`                   | Status  | Notes                                                                                                                     |
| ------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| Mainline                  | Works   |                                                                                                                           |
| CPU                       | Works   |                                                                                                                           |
| RAM                       | Works   |                                                                                                                           |
| GPU                       | Broken  | No driver                                                                                                                 |
| NPU                       | Broken  | No driver                                                                                                                 |
| HW Encode                 | Broken  | No driver                                                                                                                 |
| HW Decode                 | Broken  | No driver                                                                                                                 |
| HDMI                      | Partial | EFI FB partially works (1080P@60Hz on most monitors)                                      |
| DP                        | Partial | Same as above                                                                                                             |
| USB-C DP                  | Partial | Same as above                                                                                                             |
| Storage                   | Works   | M.2 SSDs work as expected                                                                                 |
| Ethernet                  | Works   |                                                                                                                           |
| Front USB                 | Works   | Randomly dies, needs custom BredOS fork of Radxa bios                                                                     |
| Rear USB                  | Works   | Randomly dies, needs custom BredOS fork of Radxa bios                                                                     |
| Front audio               | Broken  | No driver                                                                                                                 |
| Rear audio                | Broken  | No driver                                                                                                                 |
| RTC                       | Works   | No driver                                                                                                                 |
| UART                      | Works   | `ttyS2` at boot                                                                                                           |
| PCIe                      | Partial | Works fine for most devices but some GPUs don't work as expected. <br> Freezes the whole system sometimes |
| M.2 E Key | Works   |                                                                                                                           |
| M.2 M Key | Works   |                                                                                                                           |
| Fan control               | Works   | Auto fan control, No way to control from OS                                                                               |