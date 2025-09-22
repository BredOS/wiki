---
title: Actualizar UEFI en RK3588
description: Aprenda cómo actualizar el firmware UEFI en dispositivos basados en RK35888 ejecutando BredOS
published: true
date: 2025-09-18T07:50:28.639Z
tags:
editor: markdown
dateCreated: 2025-02-23T15:28:48.131Z
---

# 1. Introducción

- El firmware UEFI para dispositivos basados en RK3588 se puede instalar a través del gestor de paquetes. Para encontrar el paquete correcto para su dispositivo específico, ejecute:

```
sudo pacman -Ss uefi
```

Esto listará todos los paquetes de firmware de UEFI disponibles. Identifique el paquete correcto para su dispositivo desde la lista. Por ejemplo:

- **Para Edge2:** `edge2-uefi`
- **Para Fy.Ub Dúo:** `fydetab-duo-uefi`
- **Para Orange Pi 5:** `orangepi-5-uefi`
- **Para Roca 5B:** `rock-5b-uefi`
- _(Y otros tal como se enumeran en la salida.)_

# 2. Descargando el firmware

- Una vez que haya identificado el paquete correcto para su dispositivo, instálelo utilizando:

```
sudo pacman -S <device-uefi-package>
```

- Por ejemplo, si estás usando un **Fy.Ub Duo**, ejecuta:

```
sudo pacman -S fydetab-duo-uefi
```

# 3. Flashear el Firmware UEFI

Después de la instalación, la imagen del firmware se ubicará en `/usr/share/edk2/<device-name>/`.

> El sistema proporcionará el comando específico para flashear el firmware.\
> El formato general del comando es:\
> El formato general del comando es: ¡Usa eso en lugar del formato **general** abajo! ¡Usa eso en lugar del formato **general** abajo!
> {.is-warning}

- Un formato **general** del comando es:

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.X.X.img of=/dev/<TARGET_DEVICE> bs=512 skip=64 seek=64 conv=notrunc
```

Reemplazar `<TARGET_DEVICE>` por el dispositivo de almacenamiento apropiado:

> - `/dev/mmcblk0` para **eMMC**
> - `/dev/mmcblk1` para **tarjeta SD**
> - `/dev/mtdblock0` para **SPI flash**
>   {.is-info}

Por ejemplo, si estás usando **eMMC storage** en un **Fy.Ub Duo**, el comando sería:

```
sudo dd if=/usr/share/edk2/fydetab-duo/fydetab-duo_UEFI_Release_v0.12.3.img of=/dev/mmcblk0 bs=512 skip=64 seek=64 conv=notrunc
```

> ✅ **¡Hecho!** El firmware UEFI de tu dispositivo ha sido actualizado.
> {.is-success}

