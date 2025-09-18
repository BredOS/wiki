---
title: para ser añadido a orion
description:
published: true
date: 2025-09-17T00:43:12.600Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:43:12.600Z
---

# Introducción

cómo cambiar a la bifurcación de bredos personalizada de las biologías de radxa

## 2 Descargar BIOS

enlace tbd

## 3. instalar

## 3.1 Usando una unidad flash USB

formato a fat32
extraer contenidos al directorio raíz
![flashdrive-listing.png](/orion/flashdrive-listing.png)
reboot go into bios then boot manager `UEFI shell` it should auto start
note for editor ask for pics, todavía no tengo la configuración de KVM

## 3.2 Usando un CH341A

## 3.2.1 Prepare

```
sudo pacman -S flashrom
```

obtener tamaño en bytes

```
du ./cix_flash_all.bin
```

```
6288062 ./cix_flash_all.bin
```

escribir

```
dd if=/dev/zero bs=1 count=$((8388608 - reemplazo)) >> ./cix_flash_all.bin
```

## 3.2.2 Hw conexión

[sata-firmware-fix](/en/itx-3588j/sata-firmware-fix) # mismas maneras

## 3.2.3 escribir

sudo flashrom -p ch341a_spi -w ./cix_flash_all.bin

