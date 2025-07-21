---
title: FydetabDuo
description:
published: true
date: 2024-11-10T19:45:29.939Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# FydetabDuo

设备支持 Cinnamon 和 KDE，但也可以使用 GNOME。

# 安装

简而言之，我们使用 "rkdeveloptool" 刷写镜像到 eMMC。命令如下：

```bash
# 首先，将设备放入遮罩模式
# 并刷入 SPI 加载器
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# 然后刷入操作系统镜像
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

详细说明请参阅 [📦 如何安装到 eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)

# 指南

- [🐾 如何在 Mali GPU 上设置 Panthor (RK3588)](/how-to/how-to-setup-panthor)
- [🎮 如何安装 Steam](/how-to/how-to-install-steam)
- [🦶 在 Fydetab 上使用 GNOME](/fydetab-duo/gnome)
- [📦 如何安装到 eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [🔧 fydetabduo wiki 中的更多信息](https://wiki.fydetabduo.com/category/-bredos)
