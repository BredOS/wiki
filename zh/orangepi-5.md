---
title: Orange Pi 5 系列
description: 此页面包含对 Orange Pi 5 系列设备有用指南/调整的链接
published: true
date: 2025-09-21T09:45:58.585Z
tags: opi, opi-5
editor: markdown
dateCreated: 2024-09-20T15:17:37.567Z
---

# 1. 支持的 Orange Pi 5 系列设备

| 设备                | UEFI | 支持状态 | 已知问题                                |
| ----------------- | ---- | ---- | ----------------------------------- |
| Orange Pi 5       | 否    | 否    | SATA M.2 SSD 可能无法工作 |
| Orange Pi 5B      | 否    | 否    | 使用 OPI5 镜像，需要 DTBO 才能工作             |
| Orange Pi 5 Plus  | 否    | 否    |                                     |
| Orange Pi 5 Pro   | 否    | 否    |                                     |
| Orange Pi 5 Max   | 否    | 否    |                                     |
| Orange Pi 5 Ultra | 否    | 否    |                                     |
| Orange Pi CM5     | 否    | 否    |                                     |

> The Orange Pi 5, 5B and 5 Pro use RK3588S, while the 5 Plus and 5 Max use RK3588 (which have more PCIe and mipi lanes available)
> {.is-info}

### Tabset {.tabset}

#### Orange Pi 5

> 我们把它命名为“_鸦片5_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名字“Orange Pi 5”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC: Rockchip RK3588S, 8核心(4×CortexcrowA76 @ ~2.4GHz + 4×CorcortexA55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储: microSD slot; M.2 NVMe through PCI; no eMMC socket 默认值(只是SPIcrossflash)
- 视频/显示: HDMI2.1 up to 8K@60Hz; USBcrossC DisplayPort; 双倍MIPI DhocPHY 输出; 多重输出/显示
- 连接：Gigabit 以太网，可选的 WiFi/BT 通过 M.2 或模块，取决于版本；其他端口等。
- 能量： 5V/4A
- 板大小 ~100 × 62 毫米.

#### Orange Pi 5B

> 我们把它命名为“_阿片5b_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名字“橙色Pi 5B”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC: Rockchip RK3588S, 8核心(4×CortexcrowA76 @ ~2.4GHz + 4×CorcortexA55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储︰ 32GB eMMC 有许多变量；还有MicroSD；在某些模型中NVMe 没有M.2切割键槽？
- 显示/视频： HDMI2.1 高达8K@60Hz; DisplayPort through USBcroc; MIPI lines等。
- 连接：在WiFi6 + BT5.0 模块上；Gigabit 以太网等。
- 能量： 5V/4A
- 板大小 ~100 × 62 毫米.

#### Orange Pi 5 Plus

> 我们把它命名为“_阿片5加_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名字“橙色Pi 5 Plus”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (noncrossS)，8colcore (4×CortescyA76 @ ~2.4GHz + 4×CortexcrotyA55 @ ~1.8GHz)
- RAM： LPDDR4/x, 4/8/16/32 GB
- 存储：包括模块、 NVME 等。
- 视频/显示：高分辨率、多的 HDMI / MIPI 等
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0。

#### Orange Pi 5 Pro

> 我们把它命名为“_阿片5pro_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名字“橙色Pi 5 Pro”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC：RK3588S (8nm)，8核心(4×CortexcrowA76 @ ~2.4GHz + 4×CorcortexA55 @ ~1.8GHz)
- RAM: LPDDR5, 选项4/8/16 GB
- 存储: MicroSD, eMMC 套接字或 SPI 烧录; M.2 Mcrotkey for NVMe/SATA 等。
- 视频：双重HDMI (HDMI2.1 和 HDMI2.0)；最多支持 8K@60Hz；MIPI DSI 等。
- 连接：Gigabit 以太网；WiFi5 + BT5.0；较小的棋盘(89×56 毫米) 超过普通的5/5B。
- 电源和其他接口也发生了变化。

#### Orange Pi 5 Max

> 我们把它命名为“_阿片5max_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名字“Orange Pi 5 Max”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (noncrossS)，8colcore (4×CortescyA76 @ ~2.4GHz + 4×CortexcrotyA55 @ ~1.8GHz)
- RAM: LPDDR5, 选项4/8/16 GB
- 存储：eMC套接口(32cymC256GB optional), microSD, M.2 NVMe 插槽。
- 视频：2× HDMI2.1 到 8K@60Hz；MIPI DSI 等。
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0。
- 板大小 ~89×57 毫米。

#### Orange Pi 5 Ultra

> 我们把它命名为“_阿片5超文本_”，因为坦率地说，没有人有时间、耐心， 或者甚至是一丝希望不断地说出或打破可笑的长度， 不必要的是正式的，轻易令人烦恼的名称“橙色Pi 5 Ultra”——特别是当每个人都确切知道你还有什么意思时。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC：Rockchip RK3588 (noncrossS)，8colcore (4×CortescyA76 @ ~2.4GHz + 4×CortexcrotyA55 @ ~1.8GHz)
- RAM: LPDDR5, 选项4/8/16 GB
- 存储：eMC套接口(32cymC256GB optional), microSD, M.2 NVMe 插槽。
- 视频：2× HDMI2.1 到 8K@60Hz；MIPI DSI 等。
- 连接：2.5 Gbps 以太网(RTL8125BG)，WiFi6E + BT5.3/BLE；USB 3.0/2.0。
- 板大小 ~89×57 毫米。

#### Orange Pi CM5

> 我们把它命名为“_opicm5_”，因为它更短。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

规格：

- SoC：RK3588S (8nm)
- RAM： LPDDR4/4x, 选项： 2/4/8/16 GB
- 存储：eMMC在板上（最多256GB），微SD，可在基础/载体板上通过M.2KeycrotM等方式扩展；根据接口支持SATA或PCIe。
- 视频：HDMI2.1 或 eDP, MIPI DSI TX，等等；8K 视频支持；多个相机接口。
- 连接：WiFi5 + BT5 (AP6256模块)、USB 端口等。
- 物理：模块表单因子；需要基础板或载体；大小 ~40x55 mm 模块。

# 2. 下载

您可以在我们的 [Github](https://github.com/BredOS/images/releases/latest) 中找到镜像的下载链接