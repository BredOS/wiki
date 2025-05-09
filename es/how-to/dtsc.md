---
title: Script de ayuda DTSC
description: Usando el script de ayuda de compilador de código fuente BredOS Device Tree
published: true
date: 2025-05-07T13:40:24.351Z
tags: null
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# Script de ayuda DTSC

`dtsc` es un comando enviado por defecto junto con BredOS junto con el paquete `bredos-tools`.
Para que funcione sin embargo necesitas instalar `dtc`, simplemente ejecuta `yay -S dtc`

El script es un envoltorio a dtsc, realizando preprocesado automático de gcc, enlazando y generando archivos necesarios.
Hace que la generación y la prueba de los árboles de dispositivos sea mucho más sencilla.
Determina y genera automáticamente árboles de dispositivos base o superposiciones en consecuencia.

## NOTA IMPORTANTE

**Instalar un árbol de dispositivo incorrecto en tu consola lo hará inoperable.**
**Ten cuidado, realiza copias de seguridad y asegura un plan de contigencia.**

# Uso

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

## Input

El script espera un archivo `.dts` de entrada. Si no se especifica ninguna salida, generó un nombre coincidente `.dtb`
El nombre del archivo de salida puede establecerse con el parámetro `-o`.

## Enlazando con el núcleo

Si tiene más de un núcleo instalado en su sistema, debe especificar la ruta del núcleo para enlazar de nuevo.
Debería verse algo así:

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

Si tiene un solo núcleo instalado, se detectará automáticamente.

## Compilando Árboles de Dispositivos Base

Si estás compilando un árbol de dispositivos base y no un overlay, necesitarás las fuentes completas de tu kernel, las cuales no son enviadas.
Esto es porque estos árboles requieren la inclusión de otros árboles de dispositivos `.dtsi`.

Para compilar tal DT, clone el repositorio de su núcleo usando git, en una ruta conocida.

Ejemplo para el núcleo `linux-rockchip-rkr3`:

```
git clone https://github.com/BredOS/linux-bredos
```

Luego ejecuta dtsc como quieras, pero con la bandera `-i`, especificando la carpeta en la que los archivos con los que quiere enlazar son.

Por ejemplo, asumiendo que queremos compilar el DT del tablero rk3588, necesitaremos especificar las opciones de la siguiente manera:

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```