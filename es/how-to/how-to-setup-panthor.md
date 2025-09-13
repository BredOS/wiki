---
title: 🐾 Cómo configurar Panthor en Mali GPUs con RK3588
description:
published: true
date: 2025-09-13T10:47:17.988Z
tags:
editor: markdown
dateCreated: 2024-31T15:03:26.994Z
---

# Habilitar Panthor en GPUs Mali con RK3588 🚀

Esta guía le guiará a través de los pasos para permitir a Panthor on Mali GPUs presentes en tablas con el chipset RK3588.

## 🎛️ 1. Activar el Panthor DTBO

### 🤖 1.1 Automáticamente

La herramienta bredos-config ofrece una forma sencilla de activar y desactivar dtbos. Iniciar la herramienta con

```
sudo bredos-config
```

y vaya a `Device Tree Manager` -> `Enable / disable overlays` y active `rockchip-rk3588-panthor-gpu`. La herramienta instala el árbol de dispositivos base y la superposición seleccionada.

> Siga cuidadosamente las instrucciones en pantalla!
> {.is-warning}

Mientras que bredos-config es capaz de instalar dtbs y alterar la configuración de grub para cargarlos en el arranque, _no_ puede alterar la configuración de uefi. Esto tiene que hacerlo el usuario. Los cambios que el usuario tiene que hacer son mostrados por bredos-config en la primera instalación de base/overlay dtbs. Los cambios también se pueden encontrar en la [Guía del árbol del dispositivo](/how-to/how-to-enable-dtbos).

### 🦶 1.2 Manualmente

Sigue la [Guía de la capa del árbol del dispositivo](/how-to/how-to-enable-dtbos) para habilitar
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`

> ¡No reinicie su sistema después de la instalación de la superposición dtb!
> {.is-warning}

## 🔄 2. Reemplazar gráficos de Panfork

Reemplaza el paquete `mesa-panfork-git` con el paquete estándar `mesa`:

```
sudo pacman -S mesa
```

## 🔁 3. Reiniciar su sistema

Instalar el cargador y controlador vulkan:

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

## 🔁 4. Reiniciar su sistema

Reiniciar el sistema para aplicar los cambios. Si quieres validar si tus gráficos, puedes ejecutar lo siguiente:

```
sudo pacman -S inxi mesa-utils
inxi -G
```