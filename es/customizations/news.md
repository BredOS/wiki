---
title: Noticias BredOS
description: Personalizar esta pieza de software sorprendentemente complicada.
published: true
date: 2025-10-05T06:49:33.972Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🎛️ 1. Introducción

Por defecto `bredos-news` se inicia cada vez que abras tu shell. Esto está establecido por una configuración en `~/.bashrc` y `/etc/profile.d/99-bredos-news.sh`.

Cada copia de `bredos-news` puede ser personalizada, lo que significa que puedes configurar completamente las características que quieres, así como temarlo completamente.

# 3. Configuración y sobrescritos

Una configuración permenant (por usuario) puede establecerse en `~/.newsrc`. Una configuración en blanco por defecto se genera automáticamente (re)después de la primera ejecución de la aplicación, para que sea posible restablecer su configuración eliminando este archivo.

- El archivo de configuración por defecto debería verse así:

```
# Configuración BredOS-Noticias

# Acento = "\033[38;5;129m"
# Accent_Segunddary = "\033[38;5; 04m"

# mañana_Actualizaciones = False
# mañana_Discos = False
# mañana_Smart = False
# Time_Tick = 0.
# Time_Refresh = 0. 5
# Onetime = False

# Atajos de configuración

# atajos = {
# "1": "bredos-config",
# }
```

> Para activar un parámetro en este archivo de configuración, elimine el <kbd>#</kbd> al comienzo de la línea.
> {.is-info}

## 2.1 Establecer acento (color)

El parámetro `Accent` establece los colores primarios, `Accent_Segundo` establece los colores para todos los detalles. Se puede aplicar cualquier secuencia de escape arbitraria ANSI.

> Para más información sobre secuencias de escape ANSI y ejemplos, siga [este enlace](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).
> {.is-info}

## 2.2 Desactivando características

| Parámetro                | Descripción                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------------- |
| `j_Updates` = `False`    | Elimina completamente la sección de actualizaciones de paquetes.                          |
| `mañana_Disco` = `False` | Elimina las notas de uso de almacenamiento medio adjuntas.                                |
| `n_h_Smart` = `False`    | Silencia las advertencias de fallo del disco. Esto **no** debe ser usado. |

## 2.3 Configurando tiempo de animación

| Parámetro               | Descripción                                                                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `Time_Tick` = `0.1`     | Configura el tiempo entre fotogramas de la animación.                                                                 |
| `Time_Refresh` = `0.25` | Configura la frecuencia con que se actualizan los detalles del sistema.                                               |
| `Onetime` = `False`     | Deshabilita el bucle de animación, el sistema de acceso directo y las funciones de redimensionamiento de la terminal. |

> Estos valores son los mejores ya existentes. No reduzca más o el uso de cpu **será** ppike.
> {.is-info}

# 4. Atajos

La matriz `shortcuts` es un diccionario de keybinds configurables. Este es básicamente un dial rápido para su terminal. Mientras que `bredos-news` está haciendo un bucle en su animación, pulsando una de las teclas configuradas, en lugar de pasar la tecla al shell, se iniciará el atajo preconfigurado.

Configurar teclas de acceso directo, como cómo se muestra en el ejemplo, permite ejecutar comandos o funciones de python. Para el ejemplo anterior, presionando <kbd>1</kbd> iniciará la herramienta `bredos-config`. Todas las operaciones de shell, como cambiar directorio y/o tubería, están totalmente soportadas, mientras que las claves especiales y combinaciones de teclas no están soportadas actualmente.

# 5. Sobreescritura del entorno

Establecer la variable `HUSH_NEWS=1` o crear el archivo `~/.hush_login` evitará que BredOS News se ejecute.
