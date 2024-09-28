---
title: 📸🔄 Btrfs Instantáneas y Rollbacks con Timeshift
description: A comprehensive guide on setting up Btrfs snapshots and system rollbacks using Timeshift
published: true
date: 2024-09-28T07:58:11.350Z
tags: null
editor: markdown
dateCreated: 2024-27-27T19:19:08.209Z
---

# 📸🔄 Btrfs Instantáneas y Rollbacks con Timeshift

**Introducción**\
La **función de instantánea** del **sistema de archivos Btrfs** puede utilizarse para realizar instantáneas y rollbacks del sistema. **Timeshift** es una aplicación gráfica fácil de usar que hace este proceso fácil!

---

# Arrancar en Snapshots Timeshift desde GRUB con grub-btrfs 🚀

Cuando está bien configurado, **grub-btrfs** te permite iniciar en **Timeshift** Btrfs instantáneas directamente desde el menú GRUB, haciendo que los rollbacks del sistema sean fáciles y rápidos.

## Paso 1: Instalar grub-btrfs 📦

Para instalar **grub-btrfs**, ejecute:

```bash
sudo pacman -S grub-btrfs
```

Una vez instalado, cada vez que se actualiza el archivo de configuración **GRUB**, se crearán automáticamente entradas de arranque GRUB para las instantáneas de Timeshift Btrfs. Puede actualizar la configuración de GRUB con:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Paso 2: Automatizar actualizaciones de configuración de GRUB ⚙️

Grub-btrfs puede automatizar el proceso de actualización de GRUB cada vez que se crea un nuevo **Snapshot** de Btrfs de Timeshift.

1. Ejecuta el siguiente comando para editar la unidad de ruta grub-btrfs:
   ```bash
   sudo systemctl edit --full grub-btrfs.path
   ```

2. Reemplazar el contenido con lo siguiente:
   ```bash
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

3. Este paso es **reversible** si es necesario, usando:
   ```bash
   systemctl revertir grub-btrfs.path
   ```

## Paso 3: Habilitar actualizaciones GRUB automáticas 🟢

Activar la actualización automática del archivo de configuración GRUB ejecutando:

```bash
sudo systemctl habilita --now grub-btrfs.path
```

Puede configurar aún más grub-btrfs editando el archivo ubicado en:

```bash
/default/grub-btrfs/config
```

---

# Instantánea automática del sistema antes de actualizar el paquete con Timeshift-autosnap ⏳

Tal vez quieras instalar **timeshift-autosnap**, que automáticamente crea Snapshots Timeshift antes de realizar cualquier actualización de paquete a través de Pacman. Esto asegura que siempre tenga un **punto de restauración** antes de que se realicen cambios en su sistema. 🛡️

## Paso 1: Instalar timeshift-autosnap 📦

Para instalar **timeshift-autosnap**, ejecute:

```bash
sudo pacman -S timeshift-autosnap
```

## Paso 2: Evitar Duplicar Actualizaciones GRUB ❌🔄

Para evitar que GRUB se actualice dos veces cuando una instantánea es creada por timeshift-autosnap, recomiendo modificar el archivo de configuración. Establece `updateGrub` a `false` editando el siguiente archivo:

```bash
sudo nano, /timeshift-autosnap.conf
```

Cambiar la línea:

```bash
updateGrub=true
```

Para:

```bash
updateGrub=false
```

---

Espero que esta guía te haya ayudado a configurar con éxito **instantáneas del sistema Btrfs** y **rollbacks** con Timeshift! 😊🔧 Tener un sistema de instantáneas robusto puede salvar tu día en caso de que algo vaya mal durante una actualización o cambio del sistema. ¡Feliz información! 🖥️✨
