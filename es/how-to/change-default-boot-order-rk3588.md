---
title: Cómo cambiar la orden de inicio predeterminada en RK3588
description: Aprenda cómo cambiar el orden de arranque por defecto en dispositivos basados en RK3588 usando la configuración del firmware UEFI
published: true
date: 2025-09-15T10:09:51.246Z
tags:
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 1. Introducción

Si necesita modificar el orden de arranque en un dispositivo basado en RK3588 ejecutando BredOS, siga estos pasos:

# 2. Acceder a la UEFI

## 2.1 Acceder al Menú de Arranque

- Enciende tu dispositivo y espera a que el logotipo de BredOS aparezca durante el arranque.
- Presione la tecla `ESC` una vez mientras el logotipo se muestra para entrar en el menú UEFI.

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

## 2.2 Navegando a la configuración del pedido de inicio

- Usa las teclas de las flechas (`n` y `n`) para seleccionar `Arranque Administrador de Mantenimiento` y presiona `Entrar`.\
  ![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

- En la siguiente pantalla, selecciona `Arranque Opciones` y presiona `Entrar`.

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

- Elige `Cambiar orden de arranque` y pulsa `Entrar`.

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

## 2.3 Modificando la Orden de Arranque

- Una vez dentro del menú de orden de arranque, pulse `Enter`.

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

- Usa la flecha hacia abajo (`. `) para desplazarte al final de la lista.

- Seleccione la entrada que desea mover a la parte superior y pulse la tecla `+` hasta que llegue a la parte superior.\
  ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

- Una vez establecido el orden de arranque deseado, presione `Entrar` para confirmar.

## 2.4 Guardando y Aplicando los Cambios

- Después de configurar el orden de arranque, presione `Y` para guardar los cambios.

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

- Salga del menú y reinicie el dispositivo para aplicar el nuevo orden de arranque.

> ¡Listo! Su dispositivo se iniciará ahora usando el nuevo orden.
> {.is-success}

