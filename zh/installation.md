---
title: BredOS 安装指南
description: null
published: true
date: 2024-08-16T10:06:04..691Z
tags: null
editor: markdown
dateCreated: 2024-07-19T00:42:37.505Z
---

# 🍞 BredOS 安装指南

## 📚 目录表

- [🔽 下载 BredOS](#downloading-bredos)
- [:comple_disk: 创建安装介质(microSD)](#creating-the-installation-media-microsd)
- [:ro火箭: 从安装媒体启动(microSD)](#booting-from the-install-media-microsd)
- [💾 安装 BredOS 到 eMC (RockChip)](#installing-bredosto emmc-rockchip)
- [💻 关注 BredOS 安装程序](#follow-bredos-installer)
- [🛠️ 初始配置](#initial-configuration)

## :downwards_按钮：下载 BredOS

从 [🌐 official website](https://bredos.org/download.html) 下载最新的 BredOS 图像。

## :coly_disk: 创建安装介质(microSD)

1. 将您的microSD卡插入您的计算机。
2. 使用 [`balenaEtcher`](https://etcher.balena.io/), `dd`, 或 [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) 将BredOS 图像写入microSD卡。

## :ro火箭: 从安装媒体启动(microSD)

1. 将microSD卡插入基于ARM的单个板电脑。
2. 连接设备上的必要外观(键盘、鼠标、显示器)和电源。
3. 设备应从microSD 卡启动并加载 BredOS 安装程序。

## 💾 安装 BredOS 到 eMMC (RockChip)

如果您想要将BredOS 安装到 eMMC 存储器，而不是使用microSD卡，请遵循以下步骤：

**:emo: 在我们开始之前，请确保你下载了以下文件：**

- [📥 Rockchip 驱动程序](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip)

- 刷写工具 **(RKDevTool vX.XX)**：您可以在以下链接中下载Windows工具：
  - [🔗 link 1](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)
  - [🔗 Alternative in case `Link 1` does not work](https://dl.radxa.com/tools/windows/)
  - [🔗 链接到版本 v2.96](https://dl.radxa.com/tools/windows/RKDevTool_Release_v2.96_zh.zip)

- SPI loader 文件，例如RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

- [BredOS 图像](#downloading-bredos).

**📂 解压缩所有文件，包括默认情况下的 BredOS 图像。 mg.xz 文件，我们必须解压缩它才能将它转换为 .img 文件。**

- 第一件事是安装我们下载的Rockchip 驱动程序。 打开`DriverAssitant_v5.0`文件夹并执行文件 `DriverInstall.exe`。 打开`DriverAssitant_v5.0`文件夹并执行文件 `DriverInstall.exe`。

- 点击\\`🟢 安装驱动器:

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Android/AOSP/install_drivers.png)

- 打开包含刷入工具的文件夹：`RKDevTool_Release_v2.96` 文件夹(请检查您已下载的名称版本)并执行工具`RKDevTool.exe`。

- 在刷入工具中设置了以下配置并点击“RUN”：
  - 选择 SPI 加载文件
  - 选择 BredOS 图像
  - 检查“由地址写入”
  - 点击`RUN`，等待进程完成

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/flashing_tool_config.png)

## 💻 关注 BredOS 安装程序

1. 按照屏幕指示完成安装过程。
2. 选择您首选的语言、键盘布局和时区。
3. 设置用户帐户和密码。
4. 完成安装并重启设备。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/breddOS_installer.jpg)

## 🛠️ 初始配置

运行 BredOS 安装程序后，您可能需要完成一些初始安装任务：

- 🌐 配置网络设置
- :countrockwise_arrows_buton: 使用软件包管理器更新系统
- 🛠️ 根据需要安装额外的软件包

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)
