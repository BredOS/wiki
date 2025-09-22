---
title: Reproducir contenido protegido DRM (instalando widevine)
description: Aprende cómo habilitar la reproducción de contenido protegido por DRM en BredOS instalando el plugin Widevine
published: true
date: 2025-09-15T11:13:42.081Z
tags:
editor: markdown
dateCreated: 2024-28T05:58:27.563Z
---

# 1. Introducción

Aprenda cómo habilitar la reproducción de contenido protegido por DRM en BredOS instalando el plugin Widevine.

# 2. Ancho

## 2.1 Instalar Widevine

- Abre tu terminal y ejecuta el siguiente comando para instalar Widevine:

```
sudo pacman -S widevine-aarch64
```

## 2.2 Reiniciar su sistema

- Después de la instalación, reinicie su sistema para asegurarse de que los cambios surten efecto.

## 2.3 Configuración de Netflix

- Para ver Netflix, necesitará falsear a su agente de usuario. Usar la siguiente cadena de agente de usuario:

```
Mozilla/5.0 (X11; CrOS aarch64 15236.80.0) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/109.0.5414.125 Safari/537.36
```

> Puedes falsear fácilmente a tu agente de usuario instalando esta extensión de Firefox: [Interruptor de cadena de usuario](https://addons.mozilla.org/en-GB/firefox/addon/user-agent-string-switcher/)
> {.is-info}


