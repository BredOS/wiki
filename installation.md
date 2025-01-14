---
title: Installation guide for BredOS
description: 
published: true
date: 2024-08-16T10:06:04.691Z
tags: 
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
1. Insert your microSD card into your computer.
2. Use a tool like [`balenaEtcher`](https://etcher.balena.io/), `dd`, or [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) to write the BredOS image to the microSD card.

## 🚀 Booting from the Installation Media (microSD)
1. Insert the microSD card into your ARM-based single board computer.
2. Connect the necessary peripherals (keyboard, mouse, monitor) and power on the device.
3. The device should boot from the microSD card and load the BredOS installer.

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
1. Follow the on-screen instructions to complete the installation process.
2. Select your preferred language, keyboard layout, and time zone.
4. Set up a user account and password.
5. Complete the installation and reboot the device.

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/bredOS_installer.jpg)

## 🛠️ Initial Configuration
After running BredOS installer you may need to complete some initial setup tasks:
- 🌐 Configure network settings
- 🔄 Update the system using the package manager
- 🛠️ Install additional software packages as needed

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)