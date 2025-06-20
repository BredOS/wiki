---
title: Proton-run
description: Explorador rápido al usar el script `proton-run` de BredOS
published: true
date: 2025-05-07T14:44:47.710Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# Usando `proton-run`

`proton-run` es un paquete publicado recientemente que te permite usar Proton Experimental de Steam para ejecutar aplicaciones de Windows x86_64 bajo BredOS ARM64.

## Requisitos

- An RK3588 system running BredOS.
- Vapor. ([Guía aquí](en/how-to/how-to-install-steam))
- Después de instalar Proton Experimental a través de Steam.
- Habiendo instalado el paquete `proton-run` (`yay -S proton-run`).

## Uso

Simplemente abra un terminal y ejecute:

```
proton-run /ruta/a/tu/windows/program.exe
```

No hay muchas aplicaciones que funcionen. Hay tres emuladores encadenados para que esto sea posible.
Pero es el estado de emulación x86.