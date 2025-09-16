---
title: Herramientas BredOS
description: Utilidades y herramientas proporcionadas por BredOS
published: true
date: 2025-09-16T10:29:53.626Z
tags:
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# 1. Introducción

Esto se envía como `bredos-tools`, compatible con cualquier arquitectura del sistema, en el repositorio `BredOS-any`.
Es una parte integral de BredOS. `bredos-tools` debe ser instalado por defecto.

- Si no lo instala con:

```
sudo pacman -S bredos-tools
```

Este paquete contiene una plétora de herramientas con el único propósito de facilitar el desarrollo, el mantenimiento y el uso general de BredOS.

# 2. Protección de contraseña GRUB

BredOS incluye una utilidad para restringir las opciones de arranque GRUB con una contraseña.
Esto evita que los usuarios no autorizados inicien entradas no predeterminadas o editen parámetros de arranque.

## 2.1 Activar contraseña GRUB

- Para habilitar la protección de contraseña de grub, ejecuta:

```
sudo grub-password
```

Se te pedirá que introduzcas y confirmes una contraseña.
Una vez establecido, sólo la entrada GRUB por defecto puede iniciarse sin autenticación.

## 2.2 Desactivar contraseña GRUB

- Para desactivar la protección de contraseña de grub, ejecuta:

```
sudo grub-password -d
```

Esto elimina la restricción de contraseña y restaura el comportamiento normal de GRUB.

> La configuración se almacena en src/grub.d/99-bredos-grub-password.
> El script regenera la configuración GRUB automáticamente mediante grub-mkconfig.
> Esto modifica `/etc/grub.d/10_linux`, no lo revierta manualmente!
> {.is-info}

# 3. Script de ayuda DTSC

- Para que funcione necesitas instalar `dtc`, simplemente ejecuta

```
yay -S dtc
```

El script es un envoltorio a dtc, realizando preprocesado automático de gcc, enlazando y generando archivos necesarios.
Hace que la generación y la prueba de los árboles de dispositivos sea mucho más sencilla.
También determina y genera automáticamente árboles de dispositivos base o superposiciones en consecuencia.

> La instalación de un árbol de dispositivos incorrecto en tu dispositivo lo hará inoperante.
> Tenga cuidado, realice copias de seguridad y asegure un plan de contigencia.
> {.is-warning}

## 3.1 Uso

- Ejecuta dtsc con el parámetro `-h` para mostrar su uso:

```
uso: dtsc [-h] [-o OUTPUT] [-i INCLUDE] [-k KERNEL] [input]

Compila un archivo Fuente del Árbol de Dispositivo (DTS) en un Blob de Árbol de Dispositivo (DTBO o DTB).

argumentos posicionales:
  archivo de entrada DTS

opciones:
  -h, --help mostrar este mensaje de ayuda y salir de
  -o, --output archivo de salida OUTPUT (por defecto: hace input_filename. tb)
  -i, --include INCLUDE
                        Fuente de archivos de árbol de dispositivos adicionales (opcional)
  -k, --kernel KERNEL Manualy especifica una ruta de código fuente del núcleo (por defecto:
                        autodetect)

Ejemplo: . compile_dts.py my_device_tree.dts -o output.dtbo
```

## 3.2 Input

El script espera un archivo `.dts` de entrada. Si no se especifica ninguna salida, generó un nombre coincidente `.dtb`
El nombre del archivo de salida puede establecerse con el parámetro `-o`.

## 3.3 Enlazando contra el núcleo

Si tiene más de un núcleo instalado en su sistema, debe especificar la ruta del núcleo para enlazar de nuevo.

- Debería verse algo así:

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

Si tiene un solo núcleo instalado, se detectará automáticamente.

## 3.4 Compilando Árboles de Dispositivos Base

Si estás compilando un árbol de dispositivos base y no un overlay, necesitarás las fuentes completas de tu kernel, las cuales no son enviadas.
Esto es porque estos árboles requieren la inclusión de otros árboles de dispositivos `.dtsi`.

Para compilar tal DT, clone el repositorio de su núcleo usando git, en una ruta conocida.

- Ejemplo para el núcleo `linux-rockchip-rkr3`:

```
git clone https://github.com/BredOS/linux-bredos
```

Luego ejecuta dtsc como quieras, pero con la bandera `-i`, especificando la carpeta en la que los archivos con los que quiere enlazar son.

- Por ejemplo, asumiendo que queremos compilar el DT del tablero rk3588, necesitaremos especificar las opciones de la siguiente manera:

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```