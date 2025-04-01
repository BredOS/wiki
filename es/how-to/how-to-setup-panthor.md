---
title: 🐾 Cómo configurar Panthor en Mali GPUs con RK3588
description: null
published: true
date: 2024-10T19:29:32.381Z
tags: null
editor: markdown
dateCreated: 2024-31T15:03:26.994Z
---

# Habilitar Panthor en GPUs Mali con RK3588 🚀

Esta guía le guiará a través de los pasos para permitir a Panthor on Mali GPUs presentes en tablas con el chipset RK3588.

# 🔧 Pasos para habilitar el Panteón

### 🎛️ 1. Activar el Panthor DTBO

Sigue la [Guía Overlay del árbol de dispositivo](https://wiki.bredos.org/en/how-to/how-to-enable-dtbos) para habilitar
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**¡No reinicia tu sistema después de copiar el DTBO!**

### 🔄 2. Reemplazar gráficos de Panfork

Reemplaza el paquete `mesa-panfork-git` con el paquete estándar `mesa`:

```
sudo pacman -S mesa
```

### 🔁 3. Reiniciar su sistema

Si quieres validar si tus gráficos, puedes ejecutar lo siguiente:

```
sudo pacman -S inxi mesa-utils
inxi -G
```