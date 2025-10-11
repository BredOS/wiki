---
title: Instalación con una imagen específica del dispositivo
description:
published: false
date: 2025-10-11T09:41:50.711Z
tags:
editor: markdown
dateCreated: 2025-10-11T08:42:36.971Z
---

# 🎛️ 1. 📥 Instalar el Firmware

Para la instalación de BredOS proporcionamos imágenes específicas del dispositivo que están diseñadas para trabajar fuera de la caja para su dispositivo específico. Esto distingue estas imágenes de la instalación a través de una imagen ISO. La instalación a través de una imagen ISO es mucho más genérica, pero está soportada más allá del dispositivo que ofrecemos.

> Si no puede encontrar su dispositivo en nuestro sitio de descarga y su dispositivo soporta arranque a través de UEFI, siéntase libre de probar la instalación de ISO.
> {.is-danger}

# 3. Descargar

¡Puedes encontrar enlaces de descarga para imágenes en nuestra [website](https://bredos.org/download.html)!

# 4. Arrancar dispositivo

- Elija el dispositivo de almacenamiento en el que desea instalar BredOS en:

### Tabset {.tabset}

#### Tarjeta SD

<details><summary><b>Con el adaptador de tarjeta SD</b></summary>

Inserta tu tarjeta SD en tu lector de tarjeta SD de tu PC y continúa con [**4.1 con el adaptador de almacenamiento**](#h-41-with-storage-adapter)

</details>

<details><summary><b>Sin el adaptador de tarjeta SD</b></summary>

Inserta tu tarjeta SD en tu SBC y continúa con la guía de acuerdo al sistema operativo de tu PC encontrado en la sección [**4.2 con RKdeveloptool**](#h-4-2-with-rkdeveloptool).

> Antes de flashear, debe establecer su dispositivo de destino a `tarjeta sd`. Para ello, echa un vistazo a [4.2 Cambiando destino flash](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target).
> {.is-danger}

</details>

#### eMMC no eliminable

<details><summary><b>Con RKdeveloptool</b></summary>

Continúa con la guía de acuerdo al sistema operativo de tu PC encontrado en la sección [**4.2 con RKdeveloptool**](#h-4-2-with-rkdeveloptool)

</details>

#### EMMC extraíble

<details><summary><b>Con eMMC a USB Adapter</b></summary>

Como casi todos los USB conocidos comúnmente se basan en el almacenamiento eMMC, existen adaptadores USB a eMMC que son USB-Sticks pero con almacenamiento eMMC extraíble. Estos pueden ser usados para flashear BredOS también. Conecte el eMMC a su Adapter como se muestra en la captura de pantalla de abajo.

<details><summary><b>USB al adaptador eMMC</b></summary>

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

Luego continúa con [**4.1 con adaptador de almacenamiento**](#h-41-with-storage-adapter).

</details>

<details><summary><b>With uSD Adapter</b></summary>
As a eMMC is basically an SD Card which is (mostly) hardwired to the SBC there are adapters you can connect your eMMC to convert them into an SD Card.

<details><summary><b>uSD Adpater y eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details><summary><b>adaptador uSD conectado al lector</b></summary>

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

</details>

Luego continúa con [**4.1 con adaptador de almacenamiento**](#h-41-with-storage-adapter).

</details>

<details><summary><b>Sin capítulo</b></summary>

Conecta tu eMMC a tu SBC y continúa con la guía según el sistema operativo de tu PC encontrado en la sección [**4.2 con RKdeveloptool**](#h-4-2-with-rkdeveloptool).

</details>

#### NVMe

<details><summary><b>Preperación - ¡DESCUENTA!</b></summary>

Como el arranque directo desde la unidad nVME no está soportado por nuestros dispositivos, necesitamos instalar UEFI en un medio diferente. Después de que la UEFI es arrancada usted es capaz de arrancar desde la unidad NVMe directamente. Para instalar UEFI en tu tarjeta SPI o SD, sigue esta guía.

</details>

<details><summary><b>Con USB Adapter</b></summary>

Conecta la unidad a tu PC mediante un adaptador USB y continúa con [**4.1 con adaptador de almacenamiento**](#h-41-with-storage-adapter). Después de flashear, conecte la unidad al puerto NVMe de su SBC.

</details>

<details><summary><b>Sin capítulo</b></summary>

Conecta tu unidad NVMe a tu SBC y continúa con la guía de acuerdo con el sistema operativo de tu PC que se encuentra en la sección [**4.2 con RKdeveloptool**](#h-4-2-with-rkdeveloptool).

> Antes de flashear, debe establecer su dispositivo de destino a `NVMe`. Para ello, echa un vistazo a [4.2 Cambiando destino flash](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target).
> {.is-danger}

</details>

# 5. Parpadeando

> Proporcionamos imágenes comprimidas como archivos .xz. ¡Asegúrate de descomprimirlos antes de parpadear!
> {.is-warning}

## 4.1 con el adaptador de almacenamiento

Existen innumerables herramientas para flashear una tarjeta sd o eMMC. En esta guía cubriremos `BalenaEtcher` y `Raspberry Pi Imager`. Ambas herramientas ofrecen soporte para Linux, macOS y Microsoft Windows.

- [BalenaEtcher](https://etcher.balena.io/)
- Flashear con Raspberry Pi Imager

## 4.2 con RKdeveloptool

Para cubrir la variedad de sistemas operativos que se pueden utilizar para esto, decidimos dividir la instalación en eMC no extraíble en estas dos guías:

- [Flashear con RKDevelop bajo Linux o macOS](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [Flashear con RKDevelop en Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
