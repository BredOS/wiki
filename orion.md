---
title: Radxa Orion Series
description: 
published: true
date: 2025-09-17T00:24:22.788Z
tags: 
editor: markdown
dateCreated: 2025-09-17T00:08:50.283Z
---

# Introduction


# Mainline support
|   `linux`    | Status      |  Notes |
|--------------|-------------|--------|
| Mainline     | Works    | |
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
| Front USB    | Works    | Randomly dies, needs custom BredOS fork of Radxa bios|
| Rear USB     | Works    | Randomly dies, needs custom BredOS fork of Radxa bios|
| Front audio  | Broken   | No driver|
| Rear audio   | Broken   | No driver|
| RTC          | Works    | No driver|
| UART         | Works    | `ttyS2` at boot|
| PCIe         | Partial  | Works fine for most devices but some GPUs don't work as expected. <br> Freezes the whole system sometimes|
| M.2 E Key    | Works    | |
| M.2 M Key    | Works    | |
| Fan control  | Works    | Auto fan control, No way to control from OS |