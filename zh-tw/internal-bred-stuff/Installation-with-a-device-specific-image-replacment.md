---
title: Installation with a device specific image
description:
published: false
date: 2025-10-11T08:42:36.971Z
tags:
editor: markdown
dateCreated: 2025-10-11T08:42:36.971Z
---

# 🎛️ 1. 📥 Installing the Firmware

For the installation of BredOS we provide device specific images which are tailored to work out of the box for its specific device. This distinguishes these images from installation via an ISO image. Installation via an ISO image is much more generic, but is supported beyond the devicesupport we offer.

> If you can't find your device on our download site and your device supports booting via UEFI, feel free to give the ISO installation a try.
> {.is-danger}

# 3. Download

You can find download links for images in our [website](https://bredos.org/download.html)!

# 4. 💽 Installation

## Board

### Tabset {.tabset}

#### SD Card

<details><summary><b>With SD Card Adapter</b></summary>

There are countless tools to flash an sd card or eMMC. In this guide we will cover `BalenaEtcher` and `Raspberry Pi Imager`. Both tools offer support for Linux, macOS and Microsoft Windows.

- [BalenaEtcher](https://etcher.balena.io/)
- Flashing with Raspberry Pi Imager

</details>

<details><summary><b>Without SD Card Adapter</b></summary>

Text

- Bullet
- Points

</details>

#### non-removeable eMMC

To cover the variety of operating systems you can use for this, we decided to split the installation to non-removable eMMC into these two guides:

- Flashing the eMMC with Linux or macOS
- [Flashing the eMMC with Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)

#### removeable eMMC

<details><summary><b>With eMMC to USB Adapter</b></summary>

- As almost all commonly known USB Sticks are based on eMMC storage there are USB to eMMC adapters out there which are USB-Sticks but with removable eMMC storage. These can be used to flash BredOS too.

<details><summary><b>USB to eMMC adapter</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

</details>

<details><summary><b>With uSD Adapter</b></summary>

- As a eMMC is basically an SD Card which is (mostly) hardwired to the SBC there are adapters you can connect your eMMC to convert them into an SD Card.

<details><summary><b>uSD Adpater and eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
- Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details><summary><b>uSD Adapter connected to reader</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

  </details>

<details><summary><b>Without Adapter</b></summary>

Text

- Bullet
- Points

</details>

</details>

#### NVMe

As direct booting from the NVMe drive is not supported by our devices we need to install UEFI to a different medium. After UEFI is booted you then are able to boot from the nVME drive directly. To install UEFI to your SPI or SD Card follow [this guide](/en/install/Installation-of-UEFI).

Connect the drive to your PC, either directly or via a USB adapter. Then use one of the recommended tools in [3.2.2 Flashing eMMC / SD Card](#h-322-flashing-emmc-sd-card), making sure to use the correct drive letter or path for your NVMe drive. After flashing connect the drive to the NVMe port of your SBC.

# 4. Flashing

There are countless tools to flash an sd card or eMMC. We recommend the use of `BalenaEtcher` or `Raspberry Pi Imager`. Both tools offer support for Linux, macOS and Microsoft Windows.

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> We provide images compressed as .xz files. Make sure you decompress them before flashing!
> {.is-warning}
