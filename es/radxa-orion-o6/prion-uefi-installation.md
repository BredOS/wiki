---
title: Actualizando UEFI en Orion O6
description:
published: false
date: 2025-09-17T06:45:47.183Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. Introducción

Esta guía te guiará a través del proceso de actualización de tu firmware `UEFI` de Radxa Orion O6 a BredOS.

# 2. Características

- Puerto USB frontal de panel fijo
- La velocidad de la CPU se ha corregido para ejecutarse con 2.6GHz
- Correcciones ACPI
- Corregir para tarjetas bluetooth/wifi
- Ssds de M.2 no desaparece al azar
- Corrección de resolución de `UEFI`

# 3. Instalación

## 3.1 Prerrequisitos

- El archivo .zip de instalación `UEFI`
- Para una actualización en su lugar -> USB con formato FAT32
- Para actualizar a través de un flasher -> Un flasher basado en CH341A

Un paquete muy práctico que incluye el flasher, el clip y otros accesorios útiles puede ser pedido aquí:
https://www.aliexpress.com/item/32263275388.html
![spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> Si el enlace ha caducado, siéntete libre de darnos una cabecera en Discord o Telegram.

## 3.2 Actualización en el lugar

Puedes instalar nuestro firmware `UEFI` desde dentro de la UEFI siguiendo estos pasos:

- Formatear el dispositivo USB a FAT32 y colocar el contenido del archivo zip en el directorio raíz de la unidad.
- El contenido de la memoria USB debe aparecer de la siguiente manera:

```
BuildOptions  
BurnImage.efi  
cix_flash_all.bin  
cix_flash_ota.bin  
FlashUpdate.efi  
Shell.efi  
startup.nsh  
VariableInfo.efi
```

- Arranca tu tablero en `UEFI`. Si tienes problemas para acceder a la configuración de UEFI, revisa [esta guía] (/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- Navega a `Boot Manager` -> `UEFI Shell` para entrar en la interfaz de línea de comandos.
- El proceso de actualización debe iniciarse automáticamente.

> Después de una actualización exitosa, apague la placa y desconecte de la fuente de alimentación durante al menos 10 segundos!
> {.is-warning}

## 3.3 Actualizar a través de flasher
