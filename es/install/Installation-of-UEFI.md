---
title: Instalación de UEFI
description:
published: true
date: 2025-10-20T05:14:21.445Z
tags:
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. Introducción

Muchos de nuestros dispositivos soportados ofrecen soporte para `UEFI`, que es una interfaz de firmware moderna que inicializa el hardware e inicia el sistema operativo. Con la ayuda de `UEFI` tu dispositivo es capaz de arrancar. para ficheros (escritos en un USB-Stick o grabados en un DVD) así como para arrancar su sistema operativo directamente desde la unidad nVME o a través de la red vía PXE.

> Múltiples instalaciones de UEFI pueden causar problemas al guardar la configuración de UEFI.
> {.is-warning}

# 2. Examine su dispositivo

Lamentablemente, no todos los dispositivos que soportamos son compatibles con el arranque `UEFI`. Además, no todos los dispositivos vienen con un chip SPI instalado.

- Para determinar de qué es capaz tu dispositivo, revisa [esta tabla] (/en/table-of-supported-devices).

# 3. Instalación

- Descarga la última versión de nuestra versión UEFI [here](https://github.com/BredOS/edk2-rk3588/releases).

## 3.1 Instalación en tarjeta SD

Descargue la última versión que coincida con su dispositivo, inserte una tarjeta SD de (casi) cualquier tamaño en su escritor y utilice la herramienta de parpadeo preferida. Recomendamos el uso de:

- [BalenaEtcher](https://etcher.balena.io/)
- [Imágen Raspberry Pi](https://github.com/raspberrypi/rpi-imager)

> ¡Inserta tu tarjeta SD en tu SBC y es bueno que vayas!
> {.is-success}

## 3.2 Instalación en SPI

> Si te has saltado 3.1, vuelve hacia atrás. ¡Este paso es necesario para flashear al chip SPI!
> Puedes quitar la tarjeta SD después de
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

Sigue los pasos abajo para instalar `UEFI` en tu chip SPI.

- Copia la última versión de nuestro `UEFI` a un USB-Stick formateado FAT32 y conéctalo a tu SBC.
- Arranca tu tablero en `UEFI` desde tu tarjeta SD. Si tienes problemas para entrar en la configuración de UEFI, comprueba [esta guía](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- Navega a `Boot Manager` -> `UEFI Shell` para entrar en la interfaz de línea de comandos.
- Listar todas las particiones legibles con el uso del comando `map`. Este comando lista todas las particiones con el esquema de nombres de `fs0:`, `fs1:`, ...
- Vaya al USB-Stick que contiene la imagen del firmware tecleando el nombre del sistema de archivos y presione `Enter` para cambiar el directorio a él. Si no está seguro de qué sistema de ficheros usar, ejecute ls fsX: para listar su contenido.

```
ls fs<your drive number here>: 
```

- Flash `UEFI` a tu chip SPI con el comando:

```
sf updatefile <FIRMWARE.img> 0x0
```

- Apaga tu SBC y retira la tarjeta SD.

## 3.3 Instalación a SPI desde dentro de BredOS

Si tu tablero ha iniciado en BredOS, es posible instalar UEFI en tu SPI siguiendo [esta guía](/en/how-to/update-uefi-rk3588). Bajo la sección [3. Flashear la versión de Firmware UEFI](/en/how-to/update-uefi-rk3588#h-3-flashing-the-uefi-firmware) usa `/dev/mtdblock0` como tu dispositivo de destino.

> Ahora su dispositivo es capaz de todos los buenos bienes UEFI!
> {.is-success}
