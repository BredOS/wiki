---
title: Modificación del Kernel
description: null
published: true
date: 2024-11-11T12:14:07.650Z
tags: null
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# Modificación del Kernel

Esta guía se centra principalmente en RK3588 y el núcleo linux-rockchip-rkr3.
Este guía, sin embargo, debe transportarse principalmente a otros núcleos.

## Repositorio del núcleo BredOS

BredOS almacena su bifurcación del núcleo linux-rockchip en:
https://github.com/BredOS/linux-rockchip

La rama usada para el núcleo rkr3 es `rk6.1-rkr3`.
La variante principal está en su lugar en `rk-mainline`.

## BredOS kernel PKGBUILD

El núcleo de The está construido y los paquetes con los PKGBUILDs de:
https://github.com/BredOS/sbc-pkgbuilds

## Directorios importantes

Dentro del repositorio `sbc-pkgbuilds` hay una carpeta llamada `linux-rockchip-rkr3`.
Debe ser usado como el directorio de trabajo actual durante la construcción.
