---
title: Dúo de Fíjaros
description: null
published: true
date: 2024-10T19:45:29.939Z
tags: null
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# Dúo de Fíjaros

El dispositivo tiene y soporta Cinnamon y KDE, pero también está disponible la posibilidad de trabajar con gnome.

# Instalación

En pocas palabras, usamos `rkdeveloptool` para flashear la imagen en el eMMC. Los comandos son los siguientes:

```bash
# primero, ponga el dispositivo en modo maskrom
# y flashee el cargador de spi
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1. 9.111.bin
# luego flash la imagen os
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

Para instrucciones detalladas, consulte [📦 Cómo instalar eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)

# Guías

- [🐾 Cómo configurar Panthor en GPUs Mali con RK3588](/es/how-to/how-to-setup-panthor)
- [🎮 Cómo instalar STEAM en BredOS](/es/how-to/how-to-install-steam)
- [🦶 GNOME en el Fydetab](/fydetab-duo/gnome)
- [📦 Cómo instalar eMMC](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
