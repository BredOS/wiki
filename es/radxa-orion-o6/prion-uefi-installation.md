---
title: Actualizando UEFI en Orion O6
description:
published: true
date: 2025-09-22T06:26:53.479Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. Introducción

- Esta guía te guiará a través del proceso de actualización de tu firmware `UEFI` de Radxa Orion O6 al BredOS.

![radxa-bios.png](/orion/radxa-bios.png)

# 2. Características

- Puerto USB del panel frontal fijado.
- La velocidad de la CPU está arreglada para funcionar realmente con 2.6GHz.
- Correcciones ACPI.
- Arreglo para tarjetas bluetooth/wifi.
- M.2 ssds no desaparece al azar.
- Corrección de resolución de `UEFI`.
- Capacidad para reducir la velocidad de enlace de PCIe.

# 3. Instalación

## 3.1 Prerrequisitos

- El archivo `UEFI` installtion .zip encontrado aquí.
- Para `3.2 in-place update` -> FAT32 formated USB Stick.
- Para `3.3 Update through flasher` -> A CH341A based flasher.

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

Si tienes problemas para arrancar la `UEFI` _Prions_ o prefieres usar un flasher sigue los siguientes pasos.

> ¡Asegúrate de que tu flasher esté ajustado a **1.8 voltios**! Utilice el adaptador 1.8V para hacer esto.
> {.is-warning}

### 3.3.1 Prepare

- Instala la herramienta `flashrom`.

 ```
 sudo pacman -S flashrom
 ```

- Desempaquetar el archivo .zip UEFI e identificar el tamaño del archivo binario UEFI.

```
du ./cix_flash_all.bin
```

- La salida le mostrará su tamaño en bytes.

```
6288062 ./cix_flash_all.bin
```

En el ejemplo anterior el tamaño del archivo es `6288062`.

- Para cumplir con las especificaciones del chip, necesitamos añadir "ceros" al final del archivo hasta que coincida con el tamaño de la ficha. Reemplazar `<your file size here>` con el tamaño del archivo desde el comando anterior.

```
dd if=/dev/zero bs=1 count=$((8388608 - <your file size here>)) >> ./cix_flash_all.bin
```

### 3.3.2 Conectar a SPI

> ¡Asegúrate de que tu tablero esté desconectado de la energía mientras se elimina o inserta el chip SPI!
> {.is-warning}

El chip SPI en el Prion está empapado para una fácil eliminación. El socket se encuentra entre la cabecera del ventilador de CPU y el puerto GPIO. Para localizar fácilmente el chip, consulte la documentación de Radxa [encontrada aquí](https://radxa.com/orion/o6/marked_orion_o6.webp).

- El socket tiene dos lazas que deben ser abiertas antes de quitar el chip.

![prion-spi-loaction-cut.png](/orion/prion-spi-loaction-cut.png)

- Retire la ficha SPI de la Prión.
- Conecte el adaptador de 1.8 voltios a su flash.
- Conecte la placa ZIF al adaptador de voltios 1.8.
- Pin 1 está marcado con un punto en la ficha. Mientras que el puerto USB del flasheador se dirige hacia usted, el pin 1 está en el lado superior izquierdo. Refiérase a la captura de pantalla de abajo para obtener la orientación correcta:

![1-8v-zif-socket-cut.jpg](/orion/1-8v-zif-socket-cut.jpg)

- Inserte el chip en el conector ZIF.

### 3.3.3 Flash nuevo Firmware

- Conecta el flasheador a tu PC y empieza a parpadear con:

```
sudo flashrom -p ch341a_spi -w ./cix_flash_all.bin 
```

> Si ve el texto "VERIFICADO", el firmware ha sido instalado correctamente.
> {.is-success}
