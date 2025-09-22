---
title: Flashing the eMMC with Microsoft Windows
description:
published: false
date: 2025-09-18T08:59:46.182Z
tags:
editor: markdown
dateCreated: 2025-09-16T09:55:34.272Z
---

# 1. 簡介

First and foremost, we're sorry to hear that you have to use Windows.
But fear not – we've got you covered anyway.
This article guides you through the process of installing `RKDevTool` and the necessary `RockChip Maskrom drivers`.

For the installation of BredOS, four things are required:

1. SPI loader file, for example for the RK3588:  [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. Device Specific Image from our [official website](https://bredos.org/download.html)
3. [RockChip Maskrom drivers](https://dl.radxa.com/tools/windows/)
4. [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool),     [Alternative Link 1](https://dl.radxa.com/tools/windows/)

# 2) 2) Drivers

We start with the installation of the [Rockchip Driver](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip). After you downloaded that .zip file, extract it to your prefered location.
Inside you will find the tool `DriverInstall.exe`. Execute it with elevated rights.

> If your are getting asked: "Do you want to allow this app to make changes to your device?", click `Yes`.
> {.is-info}

A window then will pop up. Click on `Install Driver`. The drivers will then be installed on your system.

# 3. Flash BredOS with RKDevTool

With the drivers in place we can continue with the use of [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool). Extract the .zip file and execute `RKDevTool.exe`.

In `RKDevTool` set the following configuration and click on `RUN`:

- Select the SPI loader file corresponding to your SoC
- Select the BredOS image (.img) for your SBC
- Check `Write by Address`
- Click on `RUN` and wait until the process finishes

> We provide our Images as .xz compressed files. You need to extract the containing .img file before flashing!
> {.is-warning}

Wait for it to finish the flashing process and you are good to go.

> After successful flashing proceed with [**First Setup**](/en/install/first-setup).
> {.is-success}