---
title: Árboles de dispositivos
description:
published: true
date: 2025-05-15T12:51:43.781Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# Árboles de dispositivos

Los árboles de dispositivos son un mecanismo para describir el hardware usado comúnmente en sistemas ARM y RISC-V permitiendo al núcleo descubrir y configurar dispositivos de hardware sin cambiar el código del controlador del núcleo.
A diferencia de los sistemas x86, donde las tablas ACPI permiten el descubrimiento automático de hardware y la configuración, la mayoría de los sistemas ARM necesitan tener su árbol de dispositivos modificado para declarar los cambios de hardware.

## Cambiando Árboles de Dispositivos en sistemas UEFI y Grub

Abre el archivo de configuración de grub `/etc/default/grub`.
Encuentra la línea que comienza con `GRUB_DTB=` y añade la ruta al archivo de árbol de dispositivos, por ejemplo:

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```

Luego actualiza la configuración de grub:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

**Nota:** Sólo puede haber un DTB especificado.

## Updating Device Trees in U-Boot systems with extlinux

Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`, find the line with `fdt`, for example:

```bash
fdt /dtbs/rockchip/xxx.dtb
```

Then reboot.

**Nota:** Sólo puede haber un DTB especificado.