---
title: Proton-run
description: Explorador rápido al usar el script `proton-run` de BredOS
published: true
date: 2025-09-13T09:47:37.755Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# Usar proton-run para ejecutar aplicaciones de Windows

La herramienta `proton-run` es un paquete publicado recientemente que le permite usar el Proton Experimental de Steam para ejecutar aplicaciones x86_64 Windows bajo BredOS ARM64.

## 1. Requisitos

- An RK3588 system running BredOS.
- Vapor. ([Guía aquí](/how-to/how-to-install-steam))

## 2. Instalación

### 2.1 Instalar Steam Proton Experimental

Abre Steam y navega a tu `Biblioteca`. Haga clic en la barra de búsqueda y escriba `proton`. Elige `Proton Experimental` e instálalo. Otras versiones del protón no funcionarán.

### 2.2 Instalar proton-run

Instala `proton-run` con el comando

```
yay -S proton-run
```

## 3. Uso

Simplemente abra un terminal y ejecute:

```
proton-run /ruta/a/tu/windows/program.exe
```

> No hay muchas aplicaciones que funcionen. Hay tres emuladores encadenados para que esto sea posible.
> Pero es el estado de emulación x86.
> {.is-warning}
