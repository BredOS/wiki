---
title: Bluetooth Fix (ITX-3588J)
description: 
published: true
date: 2025-09-14T12:30:20.016Z
tags: 
editor: markdown
dateCreated: 2025-09-14T11:10:38.109Z
---

# Bluetooth Fix (ITX-3588J)
## 1. Install r58x-post-install
For now you have to replace a package with another one. This will not alter any behavouir of the itx-3588j but adds a service which will fix bluetooth at boottime.

First remove `itx-3588j-post-install`. This packages sets a needed parameter to work around a standby issue. Fear not we will fix this again.
```
sudo pacman -R itx-3588j-post-install
```

After that install `r58x-post-install`. This packages does the same fix for standby as the above but has the service `bluetooth-mekotronics` included.

```
sudo pacman -S r58x-post-install
```

## 2. Set correct UART path
The Bluetooth adapter is not attached to /dev/ttyS6 (like on the other RK3588 SBCs), but to /dev/ttyS9. You need to change the path inside the file `/usr/bin/bluetooth-fix`.
```
sudo nano /usr/bin/bluetooth-fix
```
```
#! /bin/bash

/usr/sbin/rfkill block 0
/usr/sbin/rfkill block bluetooth
/bin/sleep 2
/usr/sbin/rfkill unblock 0
/usr/sbin/rfkill unblock bluetooth

# FIXME Delay
/bin/sleep 1

brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS9
```

Change the last line to `/dev/ttyS6`.

```
brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS6
```

## 3. Enable bluetooth service
At last we need to enable the service `bluetooth-mekotronics`

```
sudo systemctl --now enable bluetooth-mekotronics
```

> That's it! Bluetooth should work fine now.
{.is-success}
