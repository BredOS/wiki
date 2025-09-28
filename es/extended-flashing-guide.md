---
title: Guía de Flashing Extendida
description: Un poco más sobre cómo usar RKDevelopTool
published: true
date: 2025-09-28T13:04:201Z
tags:
editor: markdown
dateCreated: 2025-09-28T13:02:13.948Z
---

Bueno, sólo quieres más barras de progreso en tu vida, ¿verdad?
Hemos cubierto :thumbsup: no se preocupe.

## Leyendo la información del medio de flash elegido

- `sudo rkdeveloptool rfi`

Este comando te mostrará los detalles del medio de flash elegido.
De forma predeterminada, esto normalmente es el eMMC, a menos que no esté disponible.

```
[bill88t@prion | ~/Descargas]> sudo rkdeveloptool rfi
Flash Info:
	Manufacturer: SAMSUNG, value=00
	Tamaño Flash: 14910 MB
	Tamaño Flash: 30535680 Sectores
	Tamaño del Bloque: 512 KB
	Tamaño de la página: 2 KB
	Bits ECC: 0
	Tiempo de acceso: 40
	Flash CS: Flash<0>
```

## Cambiando destino flash

¿Quieres flash / volcar no el eMMC sino una cosa diferente?

- `sudo rkdeveloptool cs 2` para elegir la tarjeta sdcard.
- `sudo rkdeveloptool cs 9` para seleccionar el chip SPINOR.
- `sudo rkdeveloptool cs 1` para seleccionar el eMMC de nuevo.

El cambio se reflejará en `sudo rkdeveloptool rfi`.