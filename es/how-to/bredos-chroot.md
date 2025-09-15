---
title: BredOS-Chroot utility
description: Una simple herramienta para montar y hacer chroot en una instalación BredOS desde un sistema secundario
published: true
date: 2025-09-15T06:05:42.545Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. Instalación

Disponible como parte del paquete `bredos-tools`. Por defecto esto debe ser instalado. Si no lo instala con

```
sudo pacman -S bredos-tools
```

## 2. Uso

Ejecuta `bredos-chroot` sin parámetros para mostrar el mensaje de ayuda.

```
Uso: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Ejemplo:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Monta la partición Btrfs dada con subvolúmenes y la partición de arranque,
luego arrastra en el sistema. Limpia después de salir de la raíz.
```

## 3. Ejemplo

Asumiendo que tienes una tarjeta SDCard de un sistema fallido, visible desde `lsblk` en **/dev/sdb**, puedes ejecutar:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

Mientras que `/dev/sdb3` es su partición raíz BredOS y `/dev/sdb2` es su partición de arranque BredOS.

Esto hará que un intérprete de comandos se convierta en un sistema roto, facilitando la reparación.

Una vez que la reparación esté completa, sólo puedes cerrar el shell escribiendo `exit` o Ctrl + D, y el sistema de archivos adjunto se desmontaría.