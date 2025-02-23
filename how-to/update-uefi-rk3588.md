---
title: How to Update UEFI on RK3588
description: Learn how to update the UEFI firmware on RK3588-based devices running BredOS
published: true
date: 2025-02-23T15:28:48.131Z
tags: 
editor: markdown
dateCreated: 2025-02-23T15:28:48.131Z
---

# 🔄 Updating UEFI on RK3588 Devices

The UEFI firmware for RK3588-based devices can be installed via the package manager. To find the correct package for your specific device, run:

```
sudo pacman -Ss uefi
```

This will list all available UEFI firmware packages. Identify the correct package for your device from the list. For example:

- **For Edge2:** `edge2-uefi`
- **For Fydetab Duo:** `fydetab-duo-uefi`
- **For Orange Pi 5:** `orangepi-5-uefi`
- **For Rock 5B:** `rock-5b-uefi`
- *(And others as listed in the output.)*

---

## 📥 Installing the Firmware

Once you have identified the correct package for your device, install it using:

```
sudo pacman -S <device-uefi-package>
```

For example, if you are using a **Fydetab Duo**, run:

```
sudo pacman -S fydetab-duo-uefi
```

---

## 🛠️ Flashing the UEFI Firmware

After installation, the firmware image will be located in `/usr/share/edk2/<device-name>/`. The system will provide the specific command to flash the firmware.  
The general format of the command is:

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/<TARGET_DEVICE> bs=512 skip=64 seek=64 conv=notrunc
```

Replace `<TARGET_DEVICE>` with the appropriate storage device:  

- `/dev/mmcblk0` for **eMMC**
- `/dev/mmcblk1` for **SD card**
- `/dev/mtdblock0` for **SPI flash**

For example, if you are using **eMMC storage** on a **Fydetab Duo**, the command would be:

```
sudo dd if=/usr/share/edk2/fydetab-duo/fydetab-duo_UEFI_Release_v0.12.3.img of=/dev/mmcblk0 bs=512 skip=64 seek=64 conv=notrunc
```

---

✅ **Done!** Your device's UEFI firmware is now updated. 🚀  
