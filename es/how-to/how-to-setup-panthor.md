---
title: 🐾 Cómo configurar Panthor en Mali GPUs con RK3588
description: null
published: true
date: 2024-09-01T16:18:22.222Z
tags: null
editor: markdown
dateCreated: 2024-31T15:03:26.994Z
---

# Habilitar Panthor en GPUs Mali con RK3588 🚀

Esta guía le guiará a través de los pasos para permitir a Panthor on Mali GPUs presentes en tablas con el chipset RK3588.

# 🔧 Pasos para habilitar el Panteón

## En dispositivos habilitados UEFI

### 🖥️ 1. Configuración inicial en UEFI

Primero, crear los directorios necesarios para los archivos DTB:

```
sudo mkdir -p /boot/dtb/{base,overlays}
```

A continuación, configure sus ajustes de UEFI. Arrancar en UEFI > Administrador de Dispositivos > Configuración de Plataforma Rockchip > ACPI / Árbol de Dispositivos, y hacer lo siguiente:

- **Establece `Modo de tabla de configuración` a `Árbol de dispositivo`**
- **Cambia `Support DTB override & overlays` a `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

Presione F10 para guardar e iniciar en su sistema (puede volver a la primera pantalla UEFI y seleccionar `Continuar`).

### 🛠️ 3. Configurar árbol de dispositivos

> Si estás usando un FydeTab Duo, copia el archivo DTB específico a la carpeta `base`:
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb /boot/dtb/base/
> sudo cp /boot/dtb/base/rk3588s-fydetab-duo.dtb /boot/dtb/base/rk3588s-tablet-12c-linux.dtb
> ```

{.is-info}

Para otros tableros basados en RK3588, reemplaza `rk3588-board.dtb` con tu nombre de dispositivo real:

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb /boot/dtb/base/
```

### 🌐 4. Configuración común para todos los tableros

Independientemente del foro que esté usando, copie el archivo de superposición DTBO para habilitar Panthor:

```
sudo cp /boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo /boot/dtb/overlays/
```

Además, necesita modificar la configuración de GRUB:

Abrir el archivo de configuración GRUB

```
sudo nano /default/grub
```

Comenta la siguiente línea añadiendo un `#` al principio:

```
# GRUB_DTB="dtbs/rockchip/rk3588s-fydetab-duo.dtb"
```

Actualizar GRUB con la nueva configuración

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🔄 5. Reemplazar mesa-panfork-git

Reemplaza el paquete `mesa-panfork-git` con el paquete estándar `mesa`:

```
sudo pacman -S mesa
```

### 🔁 6. Reiniciar su sistema

## ⚙️ En dispositivos habilitados para arranque U

### 1. Activar el Panthor DTBO

Edita el archivo de configuración `extlinux` para aplicar la superposición:

```
sudo nano /boot/extlinux/extlinux.conf
```

Añade la siguiente línea al archivo `extlinux.conf`:

```
fdtoverlays /dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo
```

### 🔄 2. Reemplazar mesa-panfork-git

Reemplaza el paquete `mesa-panfork-git` con el paquete estándar `mesa`:

```
sudo pacman -S mesa
```

### 🔁 3. Reiniciar su sistema
