---
title: Corregir Bluetooth (ITX-3588J)
description:
published: true
date: 2025-09-14T12:30:20.016Z
tags:
editor: markdown
dateCreated: 2025-09-14T11:10:38.109Z
---

# Corregir Bluetooth (ITX-3588J)

## 1. Instalar r58x-post-install

Por ahora tiene que reemplazar un paquete por otro. Esto no alterará ningún comportamiento del itx-3588j pero añade un servicio que arreglará bluetooth al arrancar.

Primero elimina `itx-3588j-post-install`. Este paquete establece un parámetro necesario para solucionar un problema de standby. No temamos que lo arreglaremos de nuevo.

```
sudo pacman -R itx-3588j-post-install
```

Después de eso instale `r58x-post-install`. Este paquete hace la misma corrección para standby que la anterior pero incluye el servicio `bluetooth-mekotronics`.

```
sudo pacman -S r58x-post-install
```

## 2. Establecer ruta de UART correcta

El adaptador Bluetooth no está conectado a /dev/ttyS6 (como en el otro RK3588 SBCs), sino a /dev/ttyS9. Necesitas cambiar la ruta dentro del archivo `/usr/bin/bluetooth-fix`.

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

brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2. cd /dev/ttyS9
```

Cambia la última línea a `/dev/ttyS6`.

```
brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS6
```

## 3. Habilitar servicio bluetooth

Por fin necesitamos habilitar el servicio `bluetooth-mekotronics`

```
sudo systemctl --ahora habilita bluetooth-mekotronics
```

> ¡Eso es todo! Bluetooth debería funcionar bien ahora.
> {.is-success}
