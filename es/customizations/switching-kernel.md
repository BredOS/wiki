---
title: Kernel cambiante
description:
published: true
date: 2025-09-16T10:40:30.464Z
tags:
editor: markdown
dateCreated: 2024-04T15:50:46.861Z
---

# 1. Eliminar el núcleo instalado

Por defecto, la mayoría de los dispositivos vienen con el núcleo `linux-rockchip-rkr3`.
Sin embargo, puede que desee cambiar de otro o a otro núcleo.

- Para hacer esto primero valida qué núcleo tiene instalado:

```
pacman -Qs linux | grep "linux"
```

- Esto mostrará una lista, como:

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

# 2. Proceda a instalar el nuevo núcleo

## 2.1 Eliminar el núcleo instalado

- Con el caso anterior el comando sería:

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

> A partir de este punto NO ES SAFE REBOOT.
> {.is-danger}

## 2.2 Proceda a instalar el nuevo núcleo

- Reemplaza `<your-new-kernel>` y `<your-new-kernel-headers>` por el paquete del núcleo de tu elección.

```
sudo pacman -S <your-new-kernel> <your-new-kernel-headers>
```

- El paquete del núcleo generará una imagen de initramfs. Puede encontrar su nombre de archivo desde el registro de instalación:

```
(14/30) Updating linux initcpios...
:: Building initramfs for linux-rockchip-rkr3 (6.1.75-rkr3)
dracut[I]: Executing: /usr/bin/dracut --force --hostonly --no-hostonly-cmdline /boot/initramfs-linux-rockchip-rkr3.img 6.1.75-rkr3
dracut[I]: 74nfs: Could not find any command of 'rpcbind portmap'!
dracut[I]: *** Including module: bash ***
dracut[I]: *** Including module: systemd ***
dracut[I]: *** Including module: systemd-ask-password ***
dracut[I]: *** Including module: systemd-battery-check ***
dracut[I]: *** Including module: systemd-cryptsetup ***
dracut[I]: *** Including module: systemd-initrd ***
dracut[I]: *** Including module: systemd-journald ***
dracut[I]: *** Including module: systemd-modules-load ***
dracut[I]: *** Including module: systemd-pcrphase ***
dracut[I]: *** Including module: systemd-sysctl ***
dracut[I]: *** Including module: systemd-tmpfiles ***
dracut[I]: *** Including module: systemd-udevd ***
dracut[I]: *** Including module: i18n ***
dracut[I]: *** Including module: systemd-sysusers ***
dracut[I]: *** Including module: btrfs ***
dracut[I]: *** Including module: crypt ***
dracut[I]: *** Including module: dm ***
dracut[I]: *** Including module: fs-lib ***
dracut[I]: *** Including module: kernel-modules ***
dracut[I]: *** Including module: kernel-modules-extra ***
dracut[I]: *** Including module: mdraid ***
dracut[I]: *** Including module: qemu ***
dracut[I]: *** Including module: qemu-net ***
dracut[I]: *** Including module: hwdb ***
dracut[I]: *** Including module: lunmask ***
dracut[I]: *** Including module: rootfs-block ***
dracut[I]: *** Including module: terminfo ***
dracut[I]: *** Including module: udev-rules ***
dracut[I]: *** Including module: virtiofs ***
dracut[I]: *** Including module: dracut-systemd ***
dracut[I]: *** Including module: initqueue ***
dracut[I]: *** Including module: usrmount ***
dracut[I]: *** Including module: base ***
dracut[I]: *** Including module: shell-interpreter ***
dracut[I]: *** Including module: shutdown ***
dracut[I]: *** Including module: btrfs-snapshot-overlay ***
dracut[I]: *** Including modules done ***
dracut[I]: *** Installing kernel module dependencies ***
dracut[I]: *** Installing kernel module dependencies done ***
dracut[I]: *** Resolving executable dependencies ***
dracut[I]: *** Resolving executable dependencies done ***
dracut[I]: *** Store current command line parameters ***
dracut[I]: *** Stripping files ***
dracut[I]: *** Stripping files done ***
dracut[I]: *** Creating image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' ***
dracut[I]: *** Hardlinking files ***
dracut[I]: *** Hardlinking files done ***
dracut[I]: Using auto-determined compression method 'zstd'
dracut[I]: *** Creating initramfs image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' done ***
dracut[I]: *** Moving image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' to '/boot/initramfs-linux-rockchip-rkr3.img' ***
dracut[I]: *** Moving image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' to '/boot/initramfs-linux-rockchip-rkr3.img' done ***
```

El núcleo `linux-rockchip-rkr3` generó la imagen initramfs-linux-rockchip-rkr3.img\\\\\` initramfs. Otros núcleos producirán diferentes nombres de archivo.

## 3. Actualizar configuración del cargador de arranque

> Si durante el encendido del tablero ves un logotipo de BredOS, estás usando UEFI.
> {.is-warning}

### 3.1 Arranque U

- Editar `/boot/extlinux/extlinux.conf`:

```
sudo nano /boot/extlinux/extlinux.conf
```

- Dentro debería ser algo así:

```
etiqueta BredOS ARM
    kernel /vmlinuz-linux-rockchip-rkr3
    initrd /initramfs-linux-rockchip-rkr3.img
    fdt /dtbs/rockchip/rk3588-blueberry-edge-v10-linux. tb

    añadir root=UUID=xxxx earlycon=uart8250,mmio32,0xfeb50000 console=ttyFIQ0 console=tty1 consoleblank=0 loglevel=0 panic=10 rootwait rw init=/sbin/init rootflags=subvol=@ rootfstype=btrfs
```

Necesita editar la línea `initrd` del núcleo para apuntar al mismo nombre de archivo (sin la ruta).
También necesita editar la línea del núcleo para que coincida con eso.

- Para verificar que el nombre del archivo es correcto, puedes listar el contenido de `/boot/`:

```
ls /boot/
dtbs  
efi  
extlinux  
grub  
initramfs-linux-rockchip-rkr3.img  
vmlinuz-linux-rockchip-rkr3
```

### 3.2 UEFI

- Ejecuta lo siguiente para regenerar el grub.cfg:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

> Una vez hecho, puede reiniciar con seguridad en el nuevo núcleo.
> {.is-success}
