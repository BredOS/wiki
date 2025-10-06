---
title: Noticias BredOS
description: Personalizar esta pieza de software sorprendentemente complicada.
published: true
date: 2025-10-06T07:18:15.049Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🎛️ 1. Introducción

BredOS News se inicia cada vez que abre su shell. Esto está establecido por una configuración en `~/.bashrc` y `/etc/profile.d/99-bredos-news.sh`.

Cada copia de `bredos-news` puede ser personalizada, lo que significa que puedes configurar completamente las características que quieres, así como temarlo completamente.

# 3. Configuración y sobrescritos

La configuración permenante (por usuario) se puede hacer en `~/.newsrc`. La configuración en blanco por defecto se genera automáticamente (re)después de la primera ejecución de la aplicación.

- El archivo de configuración por defecto debería verse así:

```
"""
Configuración de noticias BredOS-

Consulte `https://wiki.bredos.org/customizations/news`,
para instrucciones detalladas sobre cómo configurar.
"""

# Acento = "\033[38;5;129m"
# Accent_seconds = "\033[38;5; 04m"

# mañana_Actualizaciones = False
# mañana_Discos = False
# mañana_Smart = False
# Time_Tick = 0.
# Time_Refresh = 0. 5
# Onetime = False

"""
Atajos de configuración

comandos de Shell, usando $SHELL, y las funciones de python están totalmente soportadas.
Sólo las teclas alfanuméricas y las teclas de símbolos pueden ser capturadas, sin combinaciones de claves.
Las claves mayúsculas funcionan y pueden estar vinculadas a separar los accesos directos de las minúsculas.
"""

accesos directos def -> Ninguno:
    print("Atajos directos configurados:")
    para i en atajos. eys():
        atajo = atajos[i]
        if is_function(atajo):
            print(f" - {i}: Función {shortcut.__name__}")
        else:
            print(f' - {i}: "{atajos directos[i]}"')
    print("\n")

atajos["1"] = "bredos-config"
atajos["0"] = "sudo sys-report"
atajos["? ] = atajos_ayuda
```

> Para activar un parámetro en este archivo de configuración, elimine el <kbd>#</kbd> al comienzo de la línea.
> {.is-info}

## 2.1 Establecer acento (color)

`Accent` establece los colores principales, `Accent_Segundo` establece los colores para todos los detalles. Se puede aplicar cualquier secuencia de escape arbitraria ANSI.

> Para más información sobre secuencias de escape ANSI y ejemplos, siga [este enlace](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).
> {.is-info}

Estilos comunes:

| Color            | Código                               |
| ---------------- | ------------------------------------ |
| Púrpura Perfecto | `Acento = "\033[38;5;129m"`         |
|                  | `Accent_Segundo= "\033[38;5;104m"`  |
| Rojo negrita     | `Acento = "\033[1m\033[38;5;124m"` |
|                  | `Accent_Segundo= "\033[38;5;160m"`  |

## Deshabilitando características

| Parámetro                | Descripción                                                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `j_Updates` = `False`    | `.h_Updates` elimina completamente la sección de actualizaciones del paquete.                        |
| `mañana_Disco` = `False` | `.h_Disks` elimina las notas de uso de almacenamiento medio adjunto.                                 |
| `n_h_Smart` = `False`    | `.h_Smart` silencia las advertencias de fallo del disco. Esto NO debe ser utilizado. |

## Configurando tiempo de animación

| Parámetro               | Descripción                                                                                                                                                                                    |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Time_Tick` = `0.1`     | Mientras que News está haciendo bucle en su animación, pulsando una de las teclas configuradas, en lugar de pasar la tecla al intérprete, se iniciará el atajo preconfigurado. |
| `Time_Refresh` = `0.25` | `Time_Refresh` configura con qué frecuencia se actualizan los detalles del sistema.                                                                                            |
| `Onetime` = `False`     | `Onetime` desactiva el bucle de animación, el sistema de acceso directo y las funciones de redimensionamiento de la terminal.                                                  |

> Estos valores son los mejores ya existentes. No reduzca más o el uso de cpu **será** ppike.
> {.is-info}

# 4. Atajos

`shortcuts` es un diccionario de keybinds configurables. Este es básicamente un dial rápido para su terminal. Mientras que `bredos-news` está haciendo un bucle en su animación, pulsando una de las teclas configuradas, en lugar de pasar la tecla al shell, se iniciará el atajo preconfigurado.

Configurar teclas, como se muestra en el ejemplo, permite ejecutar comandos o funciones de python. Para el ejemplo anterior, presionando <kbd>1</kbd> iniciará la herramienta `bredos-config`. Las operaciones de shell, como cambiar directorio y/o tuberías están totalmente soportadas. Las claves especiales y combinaciones no están soportadas actualmente.

# 5. Sobreescritura del entorno

Establecer `HUSH_NEWS=1` evitará que BredOS News se ejecute.
