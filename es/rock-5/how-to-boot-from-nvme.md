---
title: Cómo arrancar desde una unidad NVMe
description: Esta guía muestra cómo configurar el arranque desde una unidad de NVMe
published: true
date: 2025-03-05T18:13:00.890Z
tags: rock-5, rock-5b, rock-5bp, nvme
editor: markdown
dateCreated: 2024-09-21T09:09:29.723Z
---

# 🚀 Arranque BredOS de NVMe en Rock 5B/5B Plus

Para arrancar BredOS desde un SSD NVMe en la Rock 5B o Rock 5B Plus, necesitará seguir algunos pasos para preparar su dispositivo.

Estas instrucciones asumen que su Rock 5B/5B Plus ya está arrancado en Linux (ya sea desde una tarjeta eMMC o microSD) y tiene conectividad de red. Si está fuera de línea, copie los archivos necesarios a un medio externo como un dispositivo USB para acceder a ellos.

---

## 🔄 Paso 1: Actualizar Firmware UEFI

Primero, asegúrese de que tiene instalado el firmware UEFI más reciente. Puede instalar fácilmente el paquete requerido desde el repositorio BredOS.

Para la **Rock 5B Plus**, usa el siguiente comando:

```bash
sudo pacman -Sy rock-5b-uefi
```

Para la **Roca 5B**, usa esto:

```bash
sudo pacman -Sy rock-5bplus-uefi
```

## 📦 Paso 2: Flash UEFI a SPI

A continuación, necesitarás flashear el firmware UEFI en la memoria SPI de tu dispositivo.

Para la **Rock 5B Plus**, usa el siguiente comando:

```bash
sudo dd if=/usr/share/edk2/rock-5bplus/rock-5bplus_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

Para la **Roca 5B**, usa esto:

```bash
sudo dd if=/usr/share/edk2/rock-5b/rock-5b_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

## 📥 Paso 3: Escribe Imagen BredOS a NVMe

Una vez que la UEFI esté flasheada, necesitarás descargar la última imagen de BredOS del repositorio [Images](https://github.com/BredOS/images/releases). Extrae el archivo de imagen y luego usa el comando `dd` para escribir la imagen en tu SSD NVMe.

Asegúrese de reemplazar `/dev/nvme0n1` con la ruta correcta a su unidad NVMe.

```bash
sudo dd if=/ruta/a/bredos_image.img of=/dev/nvme0n1 bs=estado 4M=progreso
```

---

🎉 ¡Una vez que el proceso se haya completado, reinicie su Rock 5B/5B Plus y debería arrancar desde la SSD de NVMe!

> Do not keep the SDcard or EMMC connected when booting from NVMe as it will make it so your device wont boot!!
> {.is-warning}

