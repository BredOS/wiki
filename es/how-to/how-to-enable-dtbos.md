---
title: Cómo habilitar DTBOs
description:
published: true
date: 2025-09-16T10:44:14.092Z
tags:
editor: markdown
dateCreated: 2024-10T18:02:07.427Z
---

# 1. Introducción

Habilitar diferentes Overlays de Árbol de Dispositivos (DTBOs) permite activar modificaciones opcionales de hardware o núcleo, sin recompilar el núcleo de linux.

> Esta es también la manera deseada de alterar el comportamiento del núcleo. Por ejemplo, para habilitar la pila de gráficos panthor o desactivar el led de su sistema.
> {.is-success}

# 2. Configuración BredOS

- La herramienta bredos-config ofrece una forma sencilla de activar y desactivar dtbos. Iniciar la herramienta con

```
sudo bredos-config
```

La herramienta instala el árbol de dispositivos base y las capas seleccionadas. Luego navega a `Device Tree Manager` -> `Enable / disable overlays` y habilita las capas de dtb a tu gusto. Reiniciar su sistema para aplicar los cambios.

Mientras que bredos-config es capaz de instalar dtbs y alterar la configuración de grub para cargarlos en el arranque, _no_ puede alterar la configuración de UEFI. Esto tiene que hacerlo el usuario. Los cambios que el usuario tiene que hacer son mostrados por bredos-config en la primera instalación de base/overlay dtbs o bajo el paso con `3.4 Configurar UEFI`. Si tu consola está basada en `u-boot-based` no se necesitan más cambios.

> Si durante el encendido del tablero ves un logotipo de BredOS, estás usando UEFI.
> {.is-warning}

> Esta es la forma recomendada de activar/desactivar superposiciones de dtb. Los siguientes pasos no son necesarios si utiliza `bredos-config`.
> {.is-success}

# 3. Para sistemas impulsados por UEFI

Si se está ejecutando en un tablero impulsado por UEFI, es necesario configurarlo.
Si ya lo ha hecho antes puede saltarse al paso 5.

> Imágenes después del 12 de septiembre de 2024 use `/boot/efi` en lugar de `/boot`.
> {.is-info}

To determine where your ESP partition is located, run the command,
`df | grep "/boot" | awk '{print $NF}'` and **replace **`<ESP>`** IN ALL OF THE FOLLOWING commands** with it's output.

## 3.1 Crear los directorios necesarios para almacenar los archivos DTB

- _(Tu DTB será diferente allí)_

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

## 3.2 Copiar sobre el DTB base

> Si estás usando un FydeTab Duo, copia el archivo DTB específico a la carpeta `base`:
>
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-tablet-12c-linux.dtb

- Para otros tableros basados en RK3588, reemplaza `rk3588-board.dtb` con tu nombre de dispositivo real:

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

## 3.3 Configurar GRUB

- Abrir el archivo de configuración GRUB:

```
sudo nano /default/grub
```

- Comenta la siguiente línea añadiendo un `#` al principio:

```
# GRUB_DTB="dtbs/rockchip/device-tree.dtb"
```

- Actualizar GRUB con la nueva configuración:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 3.4 Configurar UEFI

- Reiniciar en UEFI _(Puedes hacerlo desde GRUB)_ > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`, y haz lo siguiente:

> Si necesita ayuda hay un [guide](/en/how-to/change-default-boot-order-rk3588) para cambiar el orden de arranque. En sus primeros pasos muestra cómo arrancar en la configuración de UEFI.
> {.is-info}

- Navega a `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`

- **Establece `Modo de tabla de configuración` a `Árbol de dispositivo`**

- **Cambia `Support DTB override & overlays` a `Enabled`**

![](/panthor/enable_tree_dtb_in_uefi.jpg)

- Presione F10 para guardar y reiniciar de nuevo en su sistema (puede volver a la primera pantalla UEFI y seleccionar `Continuar`).

## 3.5 Copia el DTBO

- Reemplaza `my-overlay` con el dtbo de tu elección.

```
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

## 3.6 Reboot

- Reiniciar su sistema para aplicar el cambio.

# 4. Dispositivos de arranque en U

## 4.1 Editar la configuración de extlinux

- La configuración de extlinux se puede editar ejecutando:

```
sudo nano /boot/extlinux/extlinux.conf
```

- Agrega la siguiente línea en la parte inferior del archivo, reemplazando el DTBO por el de tu elección:

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```

> **NO** añade más de una línea `fdtoverlays`.
> Si desea habilitar más de un DTBO, añádelos a una línea, separados por un espacio en blanco.
> Por ejemplo:
>
> fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
