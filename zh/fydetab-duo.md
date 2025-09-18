---
title: FydetabDuo
description:
published: true
date: 2025-09-17T10：16：17.074Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# 1. 简介

FydetabDuo是由Fyde Innovations开发的一张2hinncrow1平板电脑。 FydeOS - 基于 ChromiumhyOS 的系统 (Linuxroderived) 的制造商也可以运行 Android 应用程序。 它的设计是可以用作平板电脑，或用可防腐键盘/大小写+样式来运行更像一个小笔记本电脑。

主要规格：

- 显示：12.35点正在呈现IPS面板，分辨率~2560×1600，亮度~500牛顿。
- 处理器： ARMcrosschip RK3588S SOC。
- 内存和存储︰ 8 GB LPDDR4X RAM；存储率为128 GB eMC。 可通过微型SD扩展。
- 电池：约42小时电池寿命估计高达~10小时。
- 其他功能：Wifi 6，蓝牙 4.2，指纹传感器，立体声器，5MP 前置摄像头，样式表支持。

# 2. 下载

您可以在我们的 [website](https://bredos.org/download.html) 中找到图像的下载链接！

# 3. 安装

- 简而言之，我们使用 "rkdeveloptool" 刷写镜像到 eMMC。命令如下： 命令如下：

```bash
# 首先，将设备放入遮罩模式
# 并刷入 SPI 加载器
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# 然后刷入操作系统镜像
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

详细说明请参阅[如何安装到 eMC](https://wiki.fydetabduo.com/Available-OS/BredOS/BredOS-intro#-installation)。

# 4. 有用的链接

- [如何在马里安装带有RK3588的Panthor GPU](/how-to/how-to-setup-panthor)
- [How to Install STEAM on BredOS](/how-to/how-to-install-steam)
- [切换桌面环境](/en/how-to/switch-desktop-environments)
- [如何安装到 eMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [fydetabduo wiki中的更多信息](https://wiki.fydetabduo.com/category/-bredos)
