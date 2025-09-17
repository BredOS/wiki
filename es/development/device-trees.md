---
title: Árboles de dispositivos
description:
published: true
date: 2025-09-17T09:59:24.978Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# 1. Introducción

Los árboles de dispositivos son un mecanismo para describir el hardware usado comúnmente en sistemas ARM y RISC-V permitiendo al núcleo descubrir y configurar dispositivos de hardware sin cambiar el código del controlador del núcleo.
A diferencia de los sistemas x86, donde las tablas ACPI permiten el descubrimiento automático de hardware y la configuración, la mayoría de los sistemas ARM necesitan tener su árbol de dispositivos modificado para declarar los cambios de hardware.

# 2. Cambiando Árboles de Dispositivos

## 2.1 Cambiando Árboles de Dispositivos en sistemas UEFI y Grub

Abre el archivo de configuración de grub `/etc/default/grub`.

- Encuentra la línea que comienza con `GRUB_DTB=` y añade la ruta al archivo de árbol de dispositivos, por ejemplo:

```bash
GRUB_DTB= dtbs/rockchip/<your device tree here>.dtb
```

- Luego actualiza la configuración de grub:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

> Sólo puede haber un DTB especificado.
> {.is-info}

## 2.2 Actualizando Árboles de Dispositivos en sistemas de Arranque U con extlinux

- Edite el archivo de configuración de extlinux `/boot/extlinux/extlinux.conf`. Encuentra la línea con `fdt`, por ejemplo:

```bash
fdt /dtbs/rockchip/<your device tree here>.dtb
```

A continuación, edítala para que coincida con la ruta del árbol de tu dispositivo. Guardar y reiniciar su sistema.

> Sólo puede haber un DTB especificado.
> {.is-info}
