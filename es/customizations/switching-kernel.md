---
title: Kernel cambiante
description: null
published: false
date: 2024-04T16:21:13.994Z
tags: null
editor: markdown
dateCreated: 2024-04T15:50:46.861Z
---

# Instalando un núcleo diferente

Por defecto, la mayoría de los dispositivos vienen con el núcleo `linux-rockchip-rkr3`.
Sin embargo puede querer cambiar de otro o a otro núcleo.
Para hacer esto primero valida qué núcleo tiene instalado:

```
pacman -Qs linux | grep "linux"
```

Esto mostrará una lista, como:

```
[bill88t@duo | ~]> yay -Qs linux | grep "linux"
local/archlinux-keyring 20241203-1
local/archlinuxarm-keyring 20240419-1 (base-developer)
local/cpupower 6. 2-1 (linux-tools)
    utilidades de espacio de usuario para el sistema de archivos de linux-erofs
    Un daemon de remapado clave para linux
local/lib32-util-linux 2.40. -1
local/linux-api-headers 6.10-1
local/linux-firmware 20241111.b5885ec5-1
local/linux-firmware-whence 20241111.b5885ec5-1
local/linux-rockchip-rkr3 2:6. .75-17
local/linux-rockchip-rkr3-headers 2:6.1.75-17
local/util-linux 2.40.2-1
local/util-linux-libs 2.40.2-1
    librerías util-linux runtime
```

En la lista podemos ver linux-rockchip-rkr3 y las cabeceras que lo acompañan están instaladas.
Para instalar un núcleo diferente, primero retire el núcleo instalado, junto con sus cabezas.

## 1. Eliminar el núcleo instalado

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

A partir de este punto NO ES SAFE REBOOT.

## 2. Proceda a instalar el nuevo núcleo

```
sudo pacman -S your-new-kernel your-new-kernel-headers
```

El paquete del núcleo generará una imagen de initramfs. Puede encontrar su nombre de archivo desde el registro de instalación:

```
(14/30) Updating linux initcpios...
==> Building image from preset: /etc/mkinitcpio.d/linux-rockchip-rkr3.preset: 'default'
==> Using configuration file: '/etc/mkinitcpio.conf'
  -> -k /boot/vmlinuz-linux-rockchip-rkr3 -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-rockchip-rkr3.img
==> Starting build: '6.1.75-rkr3'
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [autodetect]
  -> Running build hook: [modconf]
  -> Running build hook: [kms]
  -> Running build hook: [keyboard]
  -> Running build hook: [keymap]
  -> Running build hook: [consolefont]
==> WARNING: consolefont: no font found in configuration
  -> Running build hook: [block]
  -> Running build hook: [filesystems]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating zstd-compressed initcpio image: '/boot/initramfs-linux-rockchip-rkr3.img'
==> Initcpio image generation successful
```