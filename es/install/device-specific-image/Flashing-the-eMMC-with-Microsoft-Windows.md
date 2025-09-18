---
title: Flashear el eMMC con Microsoft Windows
description:
published: false
date: 2025-09-18T08:59:46.182Z
tags:
editor: markdown
dateCreated: 2025-09-16T09:55:34.272Z
---

# 1. Introducción

En primer lugar, lamentamos oír que tienes que usar Windows.
Pero no el miedo, de todos modos te hemos cubierto.
Este artículo le guía a través del proceso de instalación de `RKDevTool` y los necesarios `RockChip Maskrom drivers`.

Para la instalación de BredOS, son necesarias cuatro cosas:

1. Archivo de cargador SPI, por ejemplo para el RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. Imagen específica del dispositivo de nuestro [sitio web oficial](https://bredos.org/download.html)
3. [RockChip Maskrom drivers](https://dl.radxa.com/tools/windows/)
4. [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool), [Enlace alternativo 1](https://dl.radxa.com/tools/windows/)

# 2) Conductores

Empezamos con la instalación del [Motivador de Rockchip](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip). Después de descargar ese archivo .zip, extraerlo a su ubicación preferida.
Dentro encontrará la herramienta `DriverInstall.exe`. Ejecutar con derechos elevados.

> Si te preguntan: "¿Quieres permitir que esta aplicación haga cambios en tu dispositivo?", haz clic en "Sí".
> {.is-info}

Aparecerá una ventana. Haga clic en `Install Driver`. Los controladores se instalarán en su sistema.

# 3. Flash BredOS con RKDevTool

Con los conductores en su lugar podemos continuar con el uso de [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool). Extraiga el archivo .zip y ejecute `RKDevTool.exe`.

En `RKDevTool` establece la siguiente configuración y haz clic en `RUN`:

- Seleccione el archivo de cargador SPI correspondiente a su SoC.
- Seleccione la imagen BredOS (.img) para su SBC.
- Comprueba `Escribir por Dirección`.
- Haga clic en `RUN` y espere hasta que el proceso termine.

> Proporcionamos nuestras imágenes como archivos comprimidos .xz. ¡Necesita extraer el archivo .img que contiene antes de flashear!
> {.is-warning}

Espere a que termine el proceso de parpadeo y estará listo para empezar.

> Después de flashear con éxito, proceda con [**Primera configuración**](/en/install/first-setup).
> {.is-success}