---
title: Kernel cambiante
description:
published: true
date: 2024-05T20:07:16.898Z
tags:
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

El núcleo `linux-rockchip-rkr3` generó la imagen initramfs-linux-rockchip-rkr3.img\\\` initramfs. Otros núcleos producirán diferentes nombres de archivo.

## 3. Actualizar configuración del cargador de arranque

Si durante el encendido del tablero ves un logotipo de BredOS, estás usando UEFI.

### Arrancar U

Esto sólo se aplica a los dispositivos que no arranquen con una UEFI, si usted tiene UEFI en su tabla, salte a esa sección.

Editar `/boot/extlinux/extlinux.conf`:

```
sudo nano /boot/extlinux/extlinux.conf
```

Dentro debería ser algo así:

```
etiqueta BredOS ARM
    kernel /vmlinuz-linux-rockchip-rkr3
    initrd /initramfs-linux-rockchip-rkr3.img
    fdt /dtbs/rockchip/rk3588-blueberry-edge-v10-linux. tb

    añadir root=UUID=xxxx earlycon=uart8250,mmio32,0xfeb50000 console=ttyFIQ0 console=tty1 consoleblank=0 loglevel=0 panic=10 rootwait rw init=/sbin/init rootflags=subvol=@ rootfstype=btrfs
```

Necesita editar la línea `initrd` del núcleo para apuntar al mismo nombre de archivo (sin la ruta).
También necesita editar la línea del núcleo para que coincida con eso.
Para verificar que el nombre del archivo es correcto, puedes listar el contenido de `/boot/`:

```
ls /boot/
```

### UEFI

Esta sección sólo se aplica a los dispositivos que arranquen con la UEFI. Si utiliza Arranque U en su lugar, salte a la sección anterior.

Ejecutar:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 4. Reboot

Una vez hecho, puede reiniciar con seguridad en el nuevo núcleo.