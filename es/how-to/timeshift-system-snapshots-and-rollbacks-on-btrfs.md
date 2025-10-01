---
title: Instantáneas y retrocesos Btrfs con Timeshift
description: Una guía completa sobre cómo configurar instantáneas Btrfs y retrocesos del sistema usando Timeshift
published: true
date: 2025-10-01T09:19:56.756Z
tags:
editor: markdown
dateCreated: 2024-27-27T19:19:08.209Z
---

# 1. Introducción

La función de instantánea del sistema de archivos Btrfs se puede utilizar para realizar instantáneas y retrocesos del sistema. Timeshift es una aplicación gráfica fácil de usar que hace este proceso fácil!

# 2. Arrancar en instantáneas Timeshift desde GRUB con grub-btrfs

Cuando está correctamente configurado, `grub-btrfs` le permite arrancar en instantáneas de Timeshift Btrfs directamente desde el menú GRUB, haciendo que los rollbacks del sistema sean fáciles y rápidos.

## 2.1: Instalar grub-btrfs

- Para instalar `grub-btrfs` ejecutar:

```
sudo pacman -S grub-btrfs
```

Una vez instalado, cada vez que se actualiza el archivo de configuración GRUB, se crearán automáticamente las entradas de arranque GRUB para los snapshots de Timeshift Btrfs.

- Puede actualizar la configuración de GRUB con:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 2.2: Automatizar actualizaciones de configuración GRUB

`grub-btrfs` puede automatizar el proceso de actualización de GRUB cada vez que se crea una nueva instantánea de timeshift Btrfs.

- Ejecuta el siguiente comando para editar la unidad de ruta grub-btrfs:

  ```
  sudo systemctl edit --full grub-btrfs.path
  ```

- Reemplazar el contenido con lo siguiente:
  ```
  [Unit]
  Description=Monumentos para nuevas instantáneas
  DefaultDependencies=no
  Requires=run-timeshift-backup.mount
  After=run-timeshift-backup.mount
  BindsTo=run-timeshift-backup.mount

  [Path]
  PathModified=/run/timeshift/backup/timeshift-btrfs/snapshots

  [Install][Install]
  WantedBy=run-timeshift-backup.mount
  ```

- Este paso es revertible si es necesario, utilizando:
  ```
  sudo systemctl revertir grub-btrfs.path
  ```

## 2.3: Activar Actualizaciones Automáticas GRUB

- Activar la actualización automática del archivo de configuración GRUB ejecutando:

```
sudo systemctl habilita --now grub-btrfs.path
```

- Puede configurar más grub-btrfs editando el archivo de configuración:

```
sudo nano /default/grub-btrfs/config
```

---

# 3. Instantánea automática del sistema antes de actualizar el paquete con Timeshift-autosnap

Es posible que desee instalar `timeshift-autosnap`, que automáticamente crea Snapshots Timeshift antes de realizar cualquier actualización de paquete a través de Pacman. Esto asegura que siempre tenga un punto de restauración antes de que se realicen cambios en su sistema.

## 3.1: Instalar timeshift-autosnap

- Para instalar `timeshift-autosnap` ejecutar:

```
yay -S timeshift-autosnap
```

> `timeshift-autosnap` puede requerir reiniciar tu consola antes de que funcione como se esperaba.
> {.is-warning}

## 3.2: Prevenir actualizaciones GRUB Duplicadas

Para evitar que GRUB se actualice dos veces cuando una instantánea es creada por timeshift-autosnap, Se recomienda modificar el archivo de configuración.

- Establece `updateGrub` a `false` editando el siguiente archivo:

```
sudo nano, /timeshift-autosnap.conf
```

Cambia la línea `updateGrub=true` a `updateGrub=false`.

> Tener un sistema de instantánea robusto puede salvar su día en caso de que algo vaya mal durante una actualización o cambio del sistema.
> {.is-success}

