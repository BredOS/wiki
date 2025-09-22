---
title: Dúo de Fíjaros
description:
published: true
date: 2025-09-21T09:57:45.810Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# 1. Introducción

El Fy.Ub Dúo es un tablet de 2 pulgadas desarrollado por Fyde Innovations, creadores de FydeOS — un sistema basado en Chromium OS (derivado de Linux) que también puede ejecutar aplicaciones Android. Está diseñado para ser usado como tablet o con un teclado/caja + estilo para funcionar más como un pequeño portapapeles.

Especificaciones clave:

- Visualización: 12.35�, panel IPS, resolución ~ 2560×1600, brillo ~ 500 nits.
- Procesador: Rockchip RK3588S SoC basado en ARM.
- Memoria y almacenamiento: 8 GB LPDDR4X RAM; almacenamiento es de 128 GB eMMC. Expandible a través de microSD.
- Batería de 42 Wh, duración estimada de la batería hasta ~10 horas.
- Otras características: Wi-Fi 6, Bluetooth 4.2, sensor de huella dactilar, altavoces estéreo, cámara frontal 5 MP, soporte para nosotros.

> Lo llamamos "_FydeTube_", "_FDT_", o "_Dúo_", toma tu decisión.
> {.is-info}

# 2. Descargar

¡Puedes encontrar enlaces de descarga para imágenes en nuestra [website](https://bredos.org/download.html)!

# 3. Instalación

- En pocas palabras, usamos `rkdeveloptool` para flashear la imagen en el eMMC. Los comandos son los siguientes:

```bash
# primero, ponga el dispositivo en modo maskrom
# y flashee el cargador de spi
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1. 9.111.bin
# luego flash la imagen os
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

Para obtener instrucciones detalladas, consulte [Cómo instalar eMMC](https://wiki.fydetabduo.com/Available-OS/BredOS/BredOS-intro#-installation).

# 4. Enlaces útiles

- [Cómo configurar Panthor en Mali GPUs con RK3588](/how-to/how-to-setup-panthor)
- [Cómo instalar STEAM en BredOS](/how-to/how-to-install-steam)
- [Cambiar Entorno de Escritorio](/en/how-to/switch-desktop-environments)
- [Cómo instalar eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [Más información en fydetabduo wiki](https://wiki.fydetabduo.com/category/-bredos)
