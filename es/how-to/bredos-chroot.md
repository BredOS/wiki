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

Run `bredos-chroot` without any parameters to display the help message.

```
Uso: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Ejemplo:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Monta la partición Btrfs dada con subvolúmenes y la partición de arranque,
luego arrastra en el sistema. Limpia después de salir de la raíz.
```

## 3. Example

Assuming you have a SDCard of a failed system, visible from `lsblk` at **/dev/sdb**, you can just run:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

While `/dev/sdb3` is your BredOS root partition and `/dev/sdb2` is your BredOS boot partition.

This will get a root shell into the broken system, facilitating repair.

Once repair is complete, you can just close the shell by typing `exit` or Ctrl + D, and the attached filesystem would be unmounted.