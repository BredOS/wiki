---
title: Cómo instalar vapor en ARM
description: null
published: true
date: 2024-20T08:56:15.971Z
tags: null
editor: markdown
dateCreated: 2024-20T07:04:41.476Z
---

# Instalando Steam en BredOS (ARM)

Esta guía te guiará a través del proceso de instalación de Steam en BredOS, incluyendo los pasos necesarios para agregar el repositorio multilib BredOS e instalar `box86-rk3xxx` y `box64-rk3xxx` para compatibilidad con arm.

## Tabla de contenidos

1. [Actualiza tu sistema](#step-1-update-your-system)
2. [Añadir el repositorio multi-br de BredOS](#step-2-add-the-bredos-multilib-repository)
3. [Actualizar la base de datos de Pacman](#step-3-update-the-pacman-database)
4. [Instalar Box86 y Box64](#step-4-install-box86-and-box64)
5. [Instalar Steam](#step-5-install-steam)
6. [Steam en ejecución](#step-6-running-steam)

## Paso 1: Actualice su sistema

Antes de empezar, asegúrese de que su sistema está actualizado.

```bash
sudo pacman -Syu
```

## Paso 2: Añadir el repositorio multicéntrico de BredOS

Para instalar Steam y las capas de traducción necesarias, necesita añadir el repositorio multilibrería BredOS. Abre tu archivo `/etc/pacman.conf` en un editor de texto con permisos de root.

```sh
sudo nano /etc/pacman.conf
```

Y añade las siguientes líneas al final del archivo:

```ini
[BredOS-multilib]
Inclución = Ninguno/pacman.d/bredos-mirrorlist
```

Guardar el archivo y salir del editor de texto (<kbd>Ctrl</kbd> + <kbd>X</kbd>, luego <kbd>Ctrl</kbd> + <kbd>Y</kbd>, luego <kbd>Enter</kbd>).

## Paso 3: Actualizar la base de datos de Pacman

Después de añadir el repositorio multilib, actualice la base de datos de pacman para incluir el nuevo repositorio.

```bash
sudo pacman -Syy
```

## Paso 4: Instalar Box86 y Box64

Puesto que Steam y muchos de sus juegos están construidos para la arquitectura x86, necesita instalar box86-rk3xxx y box64-rk3xxx para ejecutarlos en su dispositivo ARM.

```bash
sudo pacman -S box86-rk3xxx box64-rk3xxx
```

## Paso 5: Instalar Steam

Ahora, puede instalar Steam desde el repositorio multilib.

```bash
sudo pacman -S steam
```

## Paso 6: Steam en ejecución

Con todo lo instalado, ahora puede ejecutar Steam. Simplemente abra vapor desde el lanzador de la aplicación o escriba el siguiente comando en su terminal:

```bash
vapor
```
