---
title: 🐾 Cómo configurar Panthor en Mali GPUs con RK3588
description:
published: true
date: 2025-07-22T00:13:05.435Z
tags:
editor: markdown
dateCreated: 2024-31T15:03:26.994Z
---

# Habilitar Panthor en GPUs Mali con RK3588 🚀

Esta guía le guiará a través de los pasos para permitir a Panthor on Mali GPUs presentes en tablas con el chipset RK3588.

# 🔧 Pasos para habilitar el Panteón

### 🎛️ 1. Activar el Panthor DTBO

Sigue la [Guía de la capa del árbol del dispositivo](/how-to/how-to-enable-dtbos) para activar
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**¡No reinicie su sistema después de copiar el DTBO!**

### 🔄 2. Reemplazar gráficos de Panfork

Reemplaza el paquete `mesa-panfork-git` con el paquete estándar `mesa`:

```
sudo pacman -S mesa
```

### 🔁 3. Reiniciar su sistema

Instalar el cargador y controlador vulkan:

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

### 🔁 4. Reiniciar su sistema

Si quieres validar si tus gráficos, puedes ejecutar lo siguiente:

```
sudo pacman -S inxi mesa-utils
inxi -G
```