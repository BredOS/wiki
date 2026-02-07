---
title: Orange Pi 5 系列
description: 此页面包含对 Orange Pi 5 系列设备有用指南/调整的链接
published: true
date: 2026-02-07T14:48:31.235Z
tags: opi, opi-5
editor: markdown
dateCreated: 2024-09-20T15:17:37.567Z
---

[![sponsor-gold-tier-opi.png](/sponsors/sponsor-gold-tier-opi.png){.align-center}](http://www.orangepi.org)

# 1. 支持的 Orange Pi 5 系列设备

| 设备                | UEFI | 支持状态 | 已知问题                                |
| ----------------- | ---- | ---- | ----------------------------------- |
| Orange Pi 5       | 设备   | 否    | SATA M.2 SSD 可能无法工作 |
| Orange Pi 5B      | 设备   | 否    | 使用 OPI5 镜像，需要 DTBO 才能工作             |
| Orange Pi 5 Plus  | 设备   | 否    |                                     |
| Orange Pi 5 Pro   | 否    | 否    |                                     |
| Orange Pi 5 Max   | Yes  | 否    |                                     |
| Orange Pi 5 Ultra | Yes  | 否    |                                     |
| Orange Pi CM5     | 否    | 否    |                                     |

> The Orange Pi 5, 5B and 5 Pro use RK3588S, while the 5 Plus and 5 Max use RK3588 (which have more PCIe and mipi lanes available)
> {.is-info}

### Tabset {.tabset}

#### Orange Pi 5

> 我们把它命名为"_鸦片5_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名字"Orange Pi 5"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC: Rockchip RK3588S, 8核心(4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储: microSD 插槽; M.2 NVMe 通过 PCIe; 无 eMMC 插槽（仅 SPI flash）
- 视频/显示: HDMI2.1 最高 8K@60Hz; USB-C DisplayPort; 双 MIPI D-PHY 输出; 多输出/显示
- 连接：Gigabit 以太网，可选的 WiFi/BT 通过 M.2 或模块，取决于版本；其他端口等。
- 电源： 5V/4A
- 板大小 ~100 × 62 毫米

#### Orange Pi 5B

> 我们把它命名为"_阿片5b_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名字"Orange Pi 5B"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC: Rockchip RK3588S, 8核心(4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储︰ 32GB eMMC 有多种选项；还有 MicroSD；某些型号中有 NVMe M.2 Key-M 插槽
- 显示/视频： HDMI2.1 最高 8K@60Hz; DisplayPort 通过 USB-C; MIPI 接口等。
- 连接：WiFi6 + BT5.0 模块；Gigabit 以太网等。
- 电源： 5V/4A
- 板大小 ~100 × 62 毫米

#### Orange Pi 5 Plus

> 我们把它命名为"_阿片5加_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名字"Orange Pi 5 Plus"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (non-S)，8核心 (4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储：包括模块、NVMe 等。
- 视频/显示：高分辨率、多个 HDMI / MIPI 等
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0

#### Orange Pi 5 Pro

> 我们把它命名为"_阿片5pro_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名字"Orange Pi 5 Pro"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC：RK3588S (8nm)，8核心(4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM: LPDDR5, 可选 4/8/16 GB
- 存储: MicroSD, eMMC 插槽或 SPI 烧录; M.2 Key-M 支持 NVMe/SATA 等。
- 视频：双 HDMI (HDMI2.1 和 HDMI2.0)；最高支持 8K@60Hz；MIPI DSI 等。
- 连接：Gigabit 以太网；WiFi5 + BT5.0；较小的板子(89×56 毫米) 相比普通的5/5B。
- 电源和其他接口也有所变化。

#### Orange Pi 5 Max

> 我们把它命名为"_阿片5max_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名字"Orange Pi 5 Max"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (non-S)，8核心 (4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM: LPDDR5, 可选 4/8/16 GB
- 存储：eMMC 插槽(32GB-256GB 可选), microSD, M.2 NVMe 插槽。
- 视频：2× HDMI2.1 最高 8K@60Hz；MIPI DSI 等。
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0
- 板大小 ~89×57 毫米

> 当您想要通过 maskrom 模式刷入设备时，将 USB -A到 USB - A 电缆连接到顶部USB 3.0 (蓝色) 端口。 或者，， 你可以使用 USB-A到 USB-C 电缆，然后在 USB-C 末端将 USB-C 连接到 USB-C 适配器。
> {.is-info}

#### Orange Pi 5 Ultra

> 我们把它命名为"_阿片5超_"，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打字那可笑的长度， 不必要的正式、轻易令人烦恼的名称"Orange Pi 5 Ultra"——特别是当每个人都确切知道你在说什么的时候。
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (non-S)，8核心 (4×Cortex-A76 @ ~2.4GHz + 4×Cortex-A55 @ ~1.8GHz)
- RAM: LPDDR5, 可选 4/8/16 GB
- 存储：eMMC 插槽(32GB-256GB 可选), microSD, M.2 NVMe 插槽。
- 视频：2× HDMI2.1 最高 8K@60Hz；MIPI DSI 等。
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0
- 板大小 ~89×57 毫米

#### Orange Pi CM5

> 我们把它命名为"_opicm5_"，因为它更短。
> {.is-info}
> {.is-info}

规格：

- SoC：RK3588S (8nm)
- RAM： LPDDR4/4x, 可选： 2/4/8/16 GB
- 存储：板载 eMMC（最多256GB），microSD，可在基板/载板上通过 M.2 Key-M 等方式扩展；根据接口支持 SATA 或 PCIe。
- 视频：HDMI2.1 或 eDP, MIPI DSI TX 等；8K 视频支持；多个相机接口。
- 连接：WiFi5 + BT5 (AP6256模块)、USB 端口等。
- 物理：模块外形；需要基板或载板；模块大小 ~40x55 mm

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接

