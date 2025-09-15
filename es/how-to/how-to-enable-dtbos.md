---
title: Cómo habilitar DTBOs
description:
published: true
date: 2025-09-15T08:30:36.658Z
tags:
editor: markdown
dateCreated: 2024-10T18:02:07.427Z
---

# 1. Introducción

Habilitar diferentes Overlays de Árbol de Dispositivos (DTBOs) permite activar modificaciones opcionales de hardware o núcleo, sin recompilar el núcleo de linux.

> Esta es también la manera deseada de alterar el comportamiento del núcleo. Por ejemplo, para habilitar la pila de gráficos panthor o desactivar el led de su sistema.
> {.is-success}

# 2. Configuración BredOS

La herramienta bredos-config ofrece una forma sencilla de activar y desactivar dtbos. Iniciar la herramienta con

```
sudo bredos-config
```

y vaya a `Device Tree Manager` -> `Activar / Deshabilitar Sobreslays` y habilitar las capas de dtb a su gusto. La herramienta instala el árbol de dispositivos base y la superposición seleccionada.

> Siga cuidadosamente las instrucciones en pantalla o proced con 3.4 Configurar UEFI!
> {.is-warning}

Mientras que bredos-config es capaz de instalar dtbs y alterar la configuración de grub para cargarlos en el arranque, _no_ puede alterar la configuración de uefi. Esto tiene que hacerlo el usuario. Los cambios que el usuario tiene que hacer son mostrados por bredos-config en la primera instalación de base/overlay dtbs.

# 3. Para sistemas impulsados por UEFI

Si se está ejecutando en un tablero impulsado por UEFI, es necesario configurarlo.
Si ya lo ha hecho antes puede saltarse al paso 5.

> Imágenes después del 12 de septiembre de 2024 use `/boot/efi` en lugar de `/boot`.
> {.is-info}

To determine where your ESP partition is located, run the command,
`df | grep "/boot" | awk '{print $NF}'` and **replace **`<ESP>`** IN ALL OF THE FOLLOWING commands** with it's output.

## 3.1 Crear los directorios necesarios para almacenar los archivos DTB

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

## 3.2 Copiar sobre el DTB base

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

## 3.3 Configurar GRUB

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

## 3.4 Configurar UEFI

Reiniciar en UEFI _(Puedes hacerlo desde GRUB)_ > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`, y haz lo siguiente:

- **Establece `Modo de tabla de configuración` a `Árbol de dispositivo`**
- **Cambia `Support DTB override & overlays` a `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

Presione F10 para guardar y reiniciar de nuevo en su sistema (puede volver a la primera pantalla UEFI y seleccionar `Continuar`).

## 3.5 Copia el DTBO

Reemplaza `my-overlay` con el dtbo de tu elección.

```
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

## 3.6 Reboot

Reiniciar su sistema para aplicar el cambio.

# 4. Dispositivos de arranque en U

## 4.1 Editar la configuración de extlinux

La configuración de extlinux se puede editar ejecutando:

```
sudo nano /boot/extlinux/extlinux.conf
```

Agrega la siguiente línea en la parte inferior del archivo, reemplazando el DTBO por el de tu elección:

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```

> **NO** añade más de una línea `fdtoverlays`.
> Si desea habilitar más de un DTBO, añádelos a una línea, separados por un espacio en blanco.
> Por ejemplo:
>
> ```
> fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
> ```

{.is-warning}
