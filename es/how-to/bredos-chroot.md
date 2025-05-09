---
title: BredOS-Chroot utility
description: Una simple herramienta para montar y hacer chroot en una instalación BredOS desde un sistema secundario
published: true
date: 2025-05-07T17:48:24.068Z
tags: null
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

Disponible como parte del paquete `bredos-tools`.

## Uso

```
Uso: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Ejemplo:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Monta la partición Btrfs dada con subvolúmenes y la partición de arranque,
luego arrastra en el sistema. Limpia después de salir de la raíz.
```

Asumiendo que tienes una tarjeta SDCard de un sistema fallido, visible desde `lsblk` en /dev/sdb, puedes ejecutar:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

Y conseguirías un caparazón de raíz en el sistema roto, facilitando la reparación.

Una vez que la reparación esté completa, sólo puedes cerrar el shell escribiendo `exit` o Ctrl + D, y la tarjeta adjunta se desmontaría.