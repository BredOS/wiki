---
title: Instalación con una imagen específica del dispositivo
description:
published: false
date: 2025-09-16T05:35:58.567Z
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

- `3.1 eMC` no extraíble
- `3.2 removable eMMC y SD Card`
- `3.3 nVME`

> Antes de comenzar, por favor compruebe qué opciones están disponibles en su dispositivo!
> {.is-info}

## 3.1 eMMC no extraíble

Para cubrir la variedad de sistemas operativos que se pueden utilizar para esto, decidimos dividir la instalación en eMC no extraíble en estas dos guías:

- Flashear el eMMC con Linux o macOS
- Flashear el eMMC con Microsoft Windows

## 3.2 Tarjeta SD y eMMC extraíble

> Si usted está familiarizado con flashear Raspberry OS no necesita leer más. Simplemente coja su tarjeta SD-Card o eMMC, la imagen BredOS específica de su dispositivo y parpadee con su herramienta preferida.
> {.is-info}

En los siguientes describimos cómo flashear eMC con un adaptador. Si no posee un adaptador adecuado deje el eMMC conectado a su SBC y siga `3.1 eMC` no extraíble.

### 3.2.1 Prepare su eMMC extraíble

> Salta a `3.2.2 Flashing eMMC / SD Card` si no estás usando el almacenamiento eMMC.
> {.is-info}

#### 3.2.1.1 con adaptador uSD

- Como eMMC es básicamente una tarjeta SD que es (en su mayoría) de cable duro a la SBC hay adaptadores que puedes conectar tu eMMC para convertirlos en una tarjeta SD.

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

- Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

#### 3.2.1.2 con adaptador USB a eMMC

- Como casi todos los USB conocidos comúnmente se basan en el almacenamiento eMMC, existen adaptadores USB a eMMC que son USB-Sticks pero con almacenamiento eMMC extraíble. Estos pueden ser usados para flashear BredOS también.

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

### 3.2.2 Flashear eMMC / Tarjeta SD

Existen innumerables herramientas para flashear una tarjeta sd o eMMC. En esta guía cubriremos `BalenaEtcher` y `Raspberry Pi Imager`. Ambas herramientas ofrecen soporte para Linux, macOS y Microsoft Windows. Elige una de las guías abajo para continuar.

- Flashear con BalenaEtcher
- Flashear con Raspberry Pi Imager

## 3.3 nVME

### 3.3.1 Prerrequisitos

Como el arranque directo desde la unidad nVME no está soportado por nuestros dispositivos, necesitamos instalar UEFI en un medio diferente. Después de que UEFI es arrancado usted es capaz de arrancar desde la unidad nVME directamente. Para instalar UEFI en tu tarjeta SPI o SD, sigue esta guía.

### 3.3.2 Flashear nVME

Conecte la unidad a su PC, ya sea directamente o a través de un adaptador USB. Luego siga una de las guías en `3.2. Flashear eMMC / SD Card`, asegurándose de usar la letra de unidad correcta o la ruta de su unidad NVMe. Después de flashear, conecte la unidad al puerto nVME de su SBC.

### 3.3.3 Orden de Arranque

La UEFI debería ser capaz de tomar la unidad por sí sola. Sin embargo, el orden de los dispositivos desde los que intentará arrancar puede ralentizar el proceso de arranque o incluso fallar completamente (p. ej. si tiene un servidor PXE en su red). Para cambiar el orden de arranque siga este [guide](/en/how-to/change-default-boot-order-rk3588).

> Después de la instalación exitosa, proceda con [**Primera configuración**](/en/install/first-setup)
> {.is-success}
