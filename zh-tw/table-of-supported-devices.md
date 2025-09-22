---
title: Table of supported devices
description:
published: false
date: 2025-09-20T18:10:07.765Z
tags:
editor: markdown
dateCreated: 2025-09-16T11:31:39.039Z
---

# 1. 簡介

This page holds a table of our supported devices with known issues, hardware support and guides that apply to them.

# 2. List of devices with device spcific images

| Device                   | UEFI | SPI Chip | Known Issues                                          | Installation type                                          | Guides                              |
| ------------------------ | ---- | -------- | ----------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------- |
| Cool Pi 4 Model B        | No   | No       | Wifi doesn't work.                    | [device-specific-image](/en/install/device-specific-image) |                                     |
| FydeTab Duo              | Yes  | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Fydetab Duo](/en/fydetab-duo)      |
| Indiedroid Nova          | Yes  | No       |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| ITX-3588J                | Yes  | No       | Many, take a look at the device page                  | [device-specific-image](/en/install/device-specific-image) | [itx-3588j](/en/itx-3588j)          |
| Khadas Edge 2            | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Khadas VIM 4             | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Mekotronics R58S         | Yes  | No       |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Mekotronics R58X         | Yes  | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Mekotronics R58X-4G      | ?    | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Mekotronics R58X-Pro     | ?    | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Milk V Jupiter           | No   | Yes      | wifi doesn't work                                     | [device-specific-image](/en/install/device-specific-image) |                                     |
| Orange Pi 5              | Yes  | Yes      | Sata M.2 SSDs may not work            | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi 5B             | Yes  | Yes      | Uses OPI5 image and requires DTBO for wifi to work    | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi 5 Max          | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi 5 Plus         | Yes  | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi 5 Pro          | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi 5 Ultra        | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi CM5            | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi 5 Series](/orangepi-5)   |
| Orange Pi RV2            | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Orange Pi RV Series](/orangepi-rv) |
| Radxa CM5                | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa CM5 DTV carrier    | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa NX5 Kit            | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Radxa Rock 4C Plus       | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) |                                     |
| Radxa Rock 5 ITX         | Yes  | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5A            | Yes  | Yes[^1]  |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5B            | Yes  | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5B+           | Yes  | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5C            | Yes  | Yes[^1]  |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5D            | No   | No       |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Rock 5T            | No   | Yes      |                                                       | [device-specific-image](/en/install/device-specific-image) | [Rock 5 Series](/rock-5)            |
| Radxa Orion O6           | Yes  | Yes      | PCIe Gen 4 devices cause the board to become unstable | [Installation-with-ISO](/en/install/Installation-with-ISO) | [radxa-orion-o6](/radxa-orion-o6)   |
| {.dense} |      |          |                                                       |                                                            |                                     |

[^1]: Requires [this module](https://radxa.com/products/accessories/spi-flash-module/).