---
title: BredOS 安装指南
description:
published: true
date: 2024-08-16T10:06:04.691Z
tags:
editor: markdown
dateCreated: 2024-07-19T00:42:37.505Z
---

# 🍞 BredOS 安装指南

## 📚 目录表

- [🔽 下载 BredOS](#downloading-bredos)
- [💽 创建安装介质 (microSD)](#creating-the-installation-media-microsd)
- [🚀 从安装介质启动 (microSD)](#booting-from-the-installation-media-microsd)
- [💾 安装 BredOS 到 eMMC (RockChip)](#installing-bredos-to-emmc-rockchip)
- [💻 遵循 BredOS 安装程序](#follow-bredos-installer)
- [🛠️ 初始配置](#initial-configuration)

## 🔽 下载 BredOS

从 [🌐 官方网站](https://bredos.org/download.html) 下载适合您设备的最新 BredOS 镜像。

## 💽 创建安装介质 (microSD)

1. 将您的 microSD 卡插入您的计算机。
2. 使用 [`balenaEtcher`](https://etcher.balena.io/)、`dd` 或 [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) 等工具将 BredOS 镜像写入 microSD 卡。

## 🚀 从安装介质启动 (microSD)

1. 将 microSD 卡插入基于 ARM 的单板计算机。
2. 连接必要的外设（键盘、鼠标、显示器）并为设备通电。
3. 设备应从 microSD 卡启动并加载 BredOS 安装程序。

## 💾 安装 BredOS 到 eMMC (RockChip)

如果您想要将 BredOS 安装到 eMMC 存储器而不是使用 microSD 卡，请按照以下步骤操作：

**📝 在我们开始之前，请确保您已下载以下文件：**

- [📥 Rockchip 驱动程序](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip)

- 刷写工具 **(RKDevTool vX.XX)**：您可以通过以下链接下载 Windows 工具：
    - [🔗 链接 1](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)
    - [🔗 如果"链接 1"不起作用的备选方案](https://dl.radxa.com/tools/windows/)
    - [🔗 v2.96 版本链接](https://dl.radxa.com/tools/windows/RKDevTool_Release_v2.96_zh.zip)

- SPI 加载器文件，例如 RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

- [BredOS 镜像](#downloading-bredos)

**📂 解压缩所有文件，包括 BredOS 镜像。默认情况下是 .img.xz 文件，我们必须解压缩它才能将它转换为 .img 文件。**

- 首先安装我们下载的 Rockchip 驱动程序。打开 `DriverAssistant_v5.0` 文件夹并执行文件 `DriverInstall.exe`。 打开`DriverAssitant_v5.0`文件夹并执行文件 `DriverInstall.exe`。

- 点击 `🟢 安装驱动程序`：

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Android/AOSP/install_drivers.png)

- 打开包含刷写工具的文件夹：`RKDevTool_Release_v2.96` 文件夹（请检查您已下载的版本名称）并执行工具 `RKDevTool.exe`。

- 在刷写工具中设置以下配置并点击 "RUN"：
    - 选择 SPI 加载器文件
    - 选择 BredOS 镜像
    - 勾选 "Write by Address"
    - 点击 `RUN`，等待进程完成

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/flashing_tool_config.png)

对于 Linux 用户，您可以使用 "rkdeveloptool" 刷写镜像到 eMMC 中。命令如下： 命令如下：

```bash
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

## 💻 遵循 BredOS 安装程序

1. 按照屏幕指示完成安装过程。
2. 选择您首选的语言、键盘布局和时区。
3. 设置用户帐户和密码。
4. 完成安装并重启设备。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/breddOS_installer.jpg)

## 🛠️ 初始配置

运行 BredOS 安装程序后，您可能需要完成一些初始设置任务：

- 🌐 配置网络设置
- 🔄 使用软件包管理器更新系统
- 🛠️ 根据需要安装额外的软件包

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)