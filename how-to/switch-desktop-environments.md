---
title: Switch Desktop Environments on BredOS
description: Learn how to install and switch to the GNOME desktop environment on BredOS
published: true
date: 2025-09-17T10:14:20.331Z
tags: customization
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 1. GNOME Desktop on BredOS
## 1.1 Install Gnome

The GNOME desktop environment can be installed with the package `gnome`.  
- To install it, run:

```
pacman -S gnome
```

Additional gnome packages can be installed with `gnome-circle` which contains various extra applications extending the GNOME ecosystem and `gnome-extra` which contains development tools as well as some further applications and games that fits well into GNOME.

---

## 1.2 Switch to GDM

For proper operation, you need to switch to **GDM** after installation.  
- Run the following commands:

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

> Only GNOME on Wayland is supported.
{.is-warning}


---

## 1.3 Screen Rotation Fix

**If** your screen rotates incorrectly, you can install and configure the **Screen Rotate** extension.

### 1.3.1 Install Extension Manager

- Run:

```
sudo pacman -S extension-manager
```

Once installed, open the application.

### 1.3.2 Install Screen Rotate

Inside the application:

- Tap `Browse` > `Search`
- Type **Screen Rotate**
- Install `Screen Rotate` by **shyzus**.

### 1.3.3 Configure Screen Rotate

- Go to the `Installed` tab in Extension Manager.
- Tap the gears icon to open the extension settings.
- Increase the **Set orientation offset** value to `1`.

## 1.4 Landscape stylus usage
The stylus will only point correctly when the screen is rotated vertically by default.
To set this to instead work horizontally:

### 1.4.1 Edit udev rule
- To edit the file `fydetab.rules`, run:
```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 1.4.2 Append the configuration line
- At the bottom of the file, add:
```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1 0 0 1"
```

Then press Ctrl + S to save and Ctrl + X to quit.

# 2. Plasma Desktop on BredOS
## 2.1 Install KDE Plasma
The Plasma desktop environment can be installed with the package `plasma-desktop`.  
- To install it, run:

```
pacman -S plasma-desktop
```

This should result in a minimal installation of the plasma desktop. To install a more complete KDE experience choose either the package `plasma` (which lets you choose which plasma-related packages you want to install) or `plasma-meta` to get the full thing. Click [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) to understand the difference between a group and a meta package.

> Avoid the use of SDDM as this software is derelict! LightDM works fine with plasma.
{.is-warning}
