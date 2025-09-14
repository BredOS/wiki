---
title: Modificación del Kernel
description:
published: true
date: 2025-09-13T10:54:24.895Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# Modificación del Kernel

Esta guía se centra principalmente en RK3588 y el núcleo `linux-rockchip-rkr3`.
Este guía, sin embargo, debe transportarse principalmente a otros núcleos.

## 1. Repositorio del núcleo BredOS

BredOS almacena su `linux-rockchip` kernel fork en:
https://github.com/BredOS/linux-bredos

La rama usada para el núcleo rkr3 es `rk6.1-rkr3`.
La variante principal está en su lugar en `rk-mainline`.

## 2. BredOS kernel PKGBUILD

El núcleo está construido y los paquetes con los PKGBUILDs de:
https://github.com/BredOS/sbc-pkgbuilds

## 3. Construyendo el núcleo

Bajo sistemas ARM, sólo:

```bash
hacer -j$(nproc)
```

En sistemas x86, necesitamos compilar el núcleo de forma cruzada:

```bash
hacer ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

Deberías ver la imagen en el directorio `arch/arm64/boot/`.

## 4. Directorios importantes

Dentro del repositorio `sbc-pkgbuilds` hay una carpeta llamada `linux-rockchip-rkr3`.
Debe ser usado como el directorio de trabajo actual durante la construcción.

## 5. Compilar árboles y capas de dispositivos

Ya está disponible una guía completa para usar `dtsc`, la herramienta BredOS para compilar DTB y DTBOS.
Haga clic [here](/Tools#dtsc-helper-script) para verlo.