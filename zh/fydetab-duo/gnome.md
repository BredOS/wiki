---
title: Fydetab上的 GNOME
description: null
published: true
date: 2024-11T10：39：09.164Z
tags: null
editor: markdown
dateCreated: 2024-11-10T19：41：06.111Z
---

# FydetabDuo 上的 GNOME 桌面

gnome-desktop 可以与软件包`gnome-meta`安装。

---

为了正常操作，您也应该在安装时切换到GDM。 That can be done by running:

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

Only Gnome wayland is at all supported.

## Screen rotation fix

**If** on your Fydetab the screen rotates incorrectly, you need to install and configure the `Screen Rotate` extension.

### 1. Install Extension Manager

Run `sudo pacman -S extension-manager` to install it, and open the application.

### 2. Install Screen Rotate

After opening the app, tap `Browse` > `Search` > Type `Screen rotate` > Install `Screen Rotate` by `shyzus`.

### 3. Configure Screen Rotate

Head back to the `Installed` page of Extension Manager and tap the settings cogwheel to open the extension's settings panel.
Then you should increase the value of `Set orientation offset` to 1.

## Landscape stylus usage

The stylus will only point correctly when the screen is rotated vertically by default.
To set this to instead work horizontally:

### 1. Open `/etc/udev/rules.d/fydetab.rules`

To open the file, run:

```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 2. Append the configuration line

At the bottom of the file, add:

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1 0 0 1"
```

### 3. Reboot

After reboot the pen will work correctly.

If you mistakenly tried gnome setting's stylus calibration, remove the calibration data by running:

```
dconf reset -f /org/gnome/desktop/peripherals/tablets
```
