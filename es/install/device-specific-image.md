---
title: Instalación con una imagen específica del dispositivo
description:
published: false
date: 2025-09-21T11:42:40.378Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36:27.362Z
---

# 1. Introducción

Para la instalación de BredOS proporcionamos imágenes específicas del dispositivo que están diseñadas para trabajar fuera de la caja para su dispositivo específico. Esto distingue estas imágenes de la instalación a través de una imagen ISO. La instalación a través de una imagen ISO es mucho más genérica, pero está soportada más allá del dispositivo que ofrecemos.

> Si no puede encontrar su dispositivo en nuestro sitio de descarga y su dispositivo soporta arranque a través de UEFI, siéntase libre de probar la instalación de ISO.
> {.is-info}

# 2. Descargar

¡Puedes encontrar enlaces de descarga para imágenes en nuestra [website](https://bredos.org/download.html)!

# 3. Instalación

La instalación varía de dispositivo a dispositivo y el medio en el que desea instalar BredOS. En esta guía cubriremos la instalación a

- [3.1 eMC no extraíble](#h-31-non-removable-emmc)
- [3.2 Tarjeta SD y eMC extraíbles](#h-32-removable-emmc-and-sd-card)
- [3.3 nVME](#h-33-nvme)

> Antes de comenzar, por favor compruebe qué opciones están disponibles en su dispositivo!
> {.is-info}

## 3.1 eMMC no extraíble

Para cubrir la variedad de sistemas operativos que se pueden utilizar para esto, decidimos dividir la instalación en eMC no extraíble en estas dos guías:

- [Flashear el eMMC con Linux o macOS](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [Flashear el eMMC con Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)

## 3.2 Tarjeta SD y eMMC extraíble

> Si usted está familiarizado con flashear Raspberry OS no necesita leer más. Simplemente coja su tarjeta SD-Card o eMMC, la imagen BredOS específica de su dispositivo y parpadee con su herramienta preferida.
> {.is-info}

En los siguientes describimos cómo flashear eMC con un adaptador. Si no posees un adaptador adecuado, deja el eMMC conectado a tu SBC y sigue [3.1 eMC no extraíble](#h-31-non-removable-emmc).

### 3.2.1 Prepare su eMMC extraíble

> Saltar a [3.2.2 Flashing eMMC / SD Card](#h-322-flashing-emmc-sd-card) si no estás usando almacenamiento eMMC.
> {.is-info}

#### 3.2.1.1 con adaptador uSD

- Como eMMC es básicamente una tarjeta SD que es (en su mayoría) de cable duro a la SBC hay adaptadores que puedes conectar tu eMMC para convertirlos en una tarjeta SD.

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

- Presione firmemente el conector del eMMC al adaptador uSD y conéctelos al lector de tarjetas SD.

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

#### 3.2.1.2 con adaptador USB a eMMC

- Como casi todos los USB conocidos comúnmente se basan en el almacenamiento eMMC, existen adaptadores USB a eMMC que son USB-Sticks pero con almacenamiento eMMC extraíble. Estos pueden ser usados para flashear BredOS también.

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

### 3.2.2 Flashear eMMC / Tarjeta SD

Existen innumerables herramientas para flashear una tarjeta sd o eMMC. Recomendamos el uso de `BalenaEtcher` o `Raspberry Pi Imager`. Ambas herramientas ofrecen soporte para Linux, macOS y Microsoft Windows.

- [BalenaEtcher](https://etcher.balena.io/)
- [Imágen Raspberry Pi](https://github.com/raspberrypi/rpi-imager)

> Proporcionamos imágenes comprimidas como archivos .xz. ¡Asegúrate de descomprimirlos antes de parpadear!
> {.is-warning}

## 3.3 nVME

### 3.3.1 Preperación

Como el arranque directo desde la unidad nVME no está soportado por nuestros dispositivos, necesitamos instalar UEFI en un medio diferente. Después de que UEFI es arrancado usted es capaz de arrancar desde la unidad nVME directamente. Para instalar UEFI en tu tarjeta SPI o SD, sigue [esta guía](/en/install/Installation-of-UEFI).

### 3.3.2 Flashear nVME

Conecte la unidad a su PC, ya sea directamente o a través de un adaptador USB. Luego use una de las herramientas recomendadas en [3.2. Flashear eMMC / Tarjeta SD](#h-322-flashing-emmc-sd-card), asegurándose de usar la letra de unidad o ruta correcta para tu unidad NVMe. Después de flashear, conecte la unidad al puerto nVME de su SBC.

### 3.3.3 Orden de Arranque

La UEFI debería ser capaz de tomar la unidad por sí sola. Sin embargo, el orden de los dispositivos desde los que intentará arrancar puede ralentizar el proceso de arranque o incluso fallar completamente (p. ej. si tiene un servidor PXE en su red). Para cambiar el orden de arranque siga este [guide](/en/how-to/change-default-boot-order-rk3588).

> Después de la instalación exitosa, proceda con [**Primera configuración**](/en/install/first-setup)
> {.is-success}
