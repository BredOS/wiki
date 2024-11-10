---
title: 📟 Cómo habilitar DTBOs
description: null
published: true
date: 2024-10T19:32:58.662Z
tags: null
editor: markdown
dateCreated: 2024-10T18:02:07.427Z
---

# Cómo habilitar capas de árbol de dispositivos

**Introducción**
Habilitando diferentes capas de árboles de dispositivos (DTBOs) permite activar modificaciones de hardware o kernel opcionales, sin volver a compilar el núcleo de linux.
Esta es también la forma deseada de habilitar la pila gráfica de panthor.

---

# 💻 Para sistemas alimentados por UEFI

Si se está ejecutando en un tablero impulsado por UEFI, es necesario configurarlo.
Si ya lo ha hecho antes puede saltarse al paso 5.

> Imágenes después del 12 de septiembre de 2024 use `/boot/efi` en lugar de `/boot`.
> {.is-info}

Para determinar dónde se encuentra su partición ESP, ejecute el comando,
`df | grep "/boot" | awk '{print $NF}'` y reemplaza `<ESP>` en todos los siguientes comandos con su salida.

### 📁 1: Crear los directorios necesarios para almacenar los archivos DTB

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

### :file_gabinet: 2: Copia sobre el DTB base

> Si estás usando un FydeTab Duo, copia el archivo DTB específico a la carpeta `base`:
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tablet-12c-linux.dtb
> ```

{.is-info}

Para otros tableros basados en RK3588, reemplaza `rk3588-board.dtb` con tu nombre de dispositivo real:

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

### 🫘 3: Configurar GRUB

Abrir el archivo de configuración GRUB:

```
sudo nano /default/grub
```

Comenta la siguiente línea añadiendo un `#` al principio:

```
# GRUB_DTB="dtbs/rockchip/device-tree.dtb"
```

_(Tu DTB será diferente allí)_

Actualizar GRUB con la nueva configuración:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🎛️ 4: Configurar UEFI

Reiniciar en UEFI _(Puedes hacerlo desde GRUB)_ > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`, y haz lo siguiente:

- **Establece `Modo de tabla de configuración` a `Árbol de dispositivo`**
- **Cambia `Support DTB override & overlays` a `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

Presione F10 para guardar y reiniciar de nuevo en su sistema (puede volver a la primera pantalla UEFI y seleccionar `Continuar`).

### 🔄 5: Copiar el DTBO

Reemplaza `my-overlay` con el dtbo de tu elección.

```
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

### ► 6: Reiniciar

Reiniciar su sistema para aplicar el cambio.

# ⚙️ En dispositivos de arranque U

### 1. Editar la configuración de extlinux

La configuración de extlinux se puede editar ejecutando:

```
sudo nano /boot/extlinux/extlinux.conf
```

Agrega la siguiente línea en la parte inferior del archivo, reemplazando el DTBO por el de tu elección:

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```
