---
title: Orange Pi 5 Series
description: This page contains links to useful guides/tweaks for the OPI 5 Series devices
published: true
date: 2025-09-21T11:49:47.836Z
tags: opi, opi-5
editor: markdown
dateCreated: 2024-09-20T15:17:37.567Z
---

# 1.  Supported Orange Pi 5 Series devices
| Device            | UEFI  | Supported | Known Issues |
|-------------------|-------|-----------|--------------|
| Orange Pi 5       |  Yes    | Yes        | Sata M.2 SSDs may not work|
| Orange Pi 5B      | Yes     | Yes        |Uses OPI5 image and requires DTBO for wifi to work|
| Orange Pi 5 Plus  | Yes     | Yes        |              |
| Orange Pi 5 Pro   |No      | Yes        |              |
| Orange Pi 5 Max   |No      | Yes        |              |
| Orange Pi 5 Ultra   |No      | Yes        |              |
| Orange Pi CM5   |No      | Yes        |              |

> The Orange Pi 5, 5B and 5 Pro use RK3588S, while the 5 Plus and 5 Max use RK3588 (which have more PCIe and mipi lanes available)
{.is-info}

### Tabset {.tabset}
#### Orange Pi 5
> We nicknamed it "*opi5*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: Rockchip RK3588S, 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz) 
- RAM: LPDDR4/x, 4/8/16/32 GB 
- Storage: microSD slot; M.2 NVMe via PCIe; no eMMC socket by default (just SPI‑flash) 
- Video / Display: HDMI2.1 up to 8K@60Hz; USB‑C DisplayPort; dual MIPI D‑PHY outputs; multiple 
- Connectivity: Gigabit Ethernet, optional WiFi/BT via M.2 or modules depending on version; other ports etc.
- Power: 5V/4A 
- Board size ~100 × 62 mm.

#### Orange Pi 5B
> We nicknamed it "*opi5b*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5B" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: Rockchip RK3588S, 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz) 
- RAM: LPDDR4/x, 4/8/16/32 GB 
- Storage: 32GB eMMC on many variants; also MicroSD; no M.2‑key slot for NVMe (or limited) in some models? 
- Display/video: HDMI2.1 up to 8K@60Hz; DisplayPort via USB‑C; MIPI lines etc. 
- Connectivity: onboard WiFi6 + BT5.0 module; Gigabit Ethernet; etc.
- Power: 5V/4A 
- Board size ~100 × 62 mm.

#### Orange Pi 5 Plus
> We nicknamed it "*opi5plus*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5 Plus" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: Rockchip RK3588 (non‑S), 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB 
- Storage: includes modules, NVMe etc.
- Video / Display: high resolutions, multiple HDMI / MIPI etc.
- Connectivity: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0. 

#### Orange Pi 5 Pro
> We nicknamed it "*opi5pro*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5 Pro" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: RK3588S (8nm), 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz)
- RAM: LPDDR5, options 4/8/16 GB
- Storage: MicroSD, eMMC socket or SPI flash; M.2 M‑key for NVMe/SATA, etc. 
- Video: Dual HDMI (HDMI2.1 and HDMI2.0); support up to 8K@60Hz; MIPI DSI etc. 
- Connectivity: Gigabit Ethernet; WiFi5 + BT5.0; smaller board (89×56 mm) than regular 5/5B. 
- Power and other interfaces also shifted.

#### Orange Pi 5 Max
> We nicknamed it "*opi5max*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5 Max" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: Rockchip RK3588 (non‑S), 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz)
- RAM: LPDDR5, options 4/8/16 GB
- Storage: eMMC sockets (32‑256 GB optional), microSD, M.2 NVMe slot. 
- Video: 2× HDMI2.1 up to 8K@60Hz; MIPI DSI; etc. 
- Connectivity: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0. 
- Board size ~89×57 mm.

#### Orange Pi 5 Ultra
> We nicknamed it "*opi5ultra*" because, honestly, no one has the time, patience, or even the slightest desire to constantly say or type out the ridiculously long, unnecessarily formal, and mildly annoying name "Orange Pi 5 Ultra" — especially when everyone knows exactly what you mean anyway.
{.is-info}

Specifications:
- SoC: Rockchip RK3588 (non‑S), 8‑core (4×Cortex‑A76 @ ~2.4GHz + 4×Cortex‑A55 @ ~1.8GHz) 
- RAM: LPDDR5, options 4/8/16 GB
- Storage: eMMC sockets (32‑256 GB optional), microSD, M.2 NVMe slot. 
- Video: 2× HDMI2.1 up to 8K@60Hz; MIPI DSI; etc. 
- Connectivity: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0. 
- Board size ~89×57 mm.

#### Orange Pi CM5
> We nicknamed it "*opicm5*" because, its shorter.
{.is-info}

Specifications:
- SoC: RK3588S (8nm) 
- RAM: LPDDR4/4x, options: 2/4/8/16 GB 
- Storage: eMMC onboard (up to 256GB), microSD, expandable via M.2 Key‑M etc on base / carrier boards; support for SATA or PCIe depending on interface. 
- Video: HDMI2.1 or eDP, MIPI DSI TX, etc; 8K video support; multiple camera interfaces. 
- Connectivity: WiFi5 + BT5 (AP6256 module), USB ports etc.
- Physical: module form factor; requires base board or carrier; size ~40×55 mm module. 

# 2. Download
You can find download links for images in our [website](https://bredos.org/download.html)!