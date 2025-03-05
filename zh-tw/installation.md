---
title: Installation guide for BredOS
description: null
published: true
date: 2024-08-16T10:06:04.691Z
tags: null
editor: markdown
dateCreated: 2024-07-19T00:42:37.505Z
---

# 🍞 BredOS Installation Guide

## 📚 Table of contents

- [🔽 Downloading BredOS](#downloading-bredos)
- [💽 Creating the Installation Media (microSD)](#creating-the-installation-media-microsd)
- [🚀 Booting from the Installation Media (microSD)](#booting-from-the-installation-media-microsd)
- [💾 Installing BredOS to eMMC (RockChip)](#installing-bredos-to-emmc-rockchip)
- [💻 Follow BredOS Installer](#follow-bredos-installer)
- [🛠️ Initial Configuration](#initial-configuration)

## 🔽 Downloading BredOS

Download the latest BredOS image for your device from the [🌐 official website](https://bredos.org/download.html).

## 💽 Creating the Installation Media (microSD)

1. 將 microSD 插入您的電腦
2. Use a tool like [`balenaEtcher`](https://etcher.balena.io/), `dd`, or [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) to write the BredOS image to the microSD card.

## 🚀 Booting from the Installation Media (microSD)

1. 將 microSD 插入您的 ARM 單板電腦
2. 將必要的裝置 (鍵盤, 滑鼠, 螢幕) 接上並啟動電腦
3. 裝置將從 microSD 開機並載入 BredOS 安裝程式

## 💾 Installing BredOS to eMMC (RockChip)

If you'd like to install BredOS to eMMC storage instead of using a microSD card, follow these steps:

**📝 Before we begin, make sure you have the following files downloaded:**

- [📥 Rockchip Driver](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip)

- Flashing tool **(RKDevTool vX.XX)**: You can download the tools for Windows in the following links:
    - [🔗 Link 1](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)
    - [🔗 Alternative in case `Link 1` doesn't work](https://dl.radxa.com/tools/windows/)
    - [🔗 Link to version v2.96](https://dl.radxa.com/tools/windows/RKDevTool_Release_v2.96_zh.zip)

- SPI loader file, for example for the RK3588:  [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

- [BredOS image](#downloading-bredos).

**📂 Unzip all files including the BredOS image which by default comes in an .img.xz file and we have to unzip it to convert it into an .img file.**

- The first thing to do is installing the Rockchip Driver we have downloaded. For this, open the `DriverAssitant_v5.0` folder and execute the file `DriverInstall.exe`.

- Click on `🟢 Install Driver`:

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Android/AOSP/install_drivers.png)

- Open the folder that contains the flashing tool:  `RKDevTool_Release_v2.96` folder (check the version you have downloaded for the name) and execute the tool `RKDevTool.exe`.

- In the flashing tool set the following configuration and click on `RUN`:
    - Select the SPI loader file
    - Select the BredOS image
    - Check `Write by Address`
    - Click on `RUN` and wait until the process finishes

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/flashing_tool_config.png)

for Linux users, you can use the `rkdeveloptool` to flash the image to the eMMC. Commands are as follows:

```bash
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

## 💻 Follow BredOS Installer

1. 依照畫面上的指示完成安裝
2. 選取您偏好的語言, 鍵盤配置及時區
3. 設定使用者帳戶及密碼
4. 完成安裝並重新啟動電腦

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/bredOS_installer.jpg)

## 🛠️ Initial Configuration

After running BredOS installer you may need to complete some initial setup tasks:

- 🌐 Configure network settings
- 🔄 Update the system using the package manager
- 🛠️ Install additional software packages as needed

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)