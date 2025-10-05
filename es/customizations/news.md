---
title: Noticias BredOS
description: Personalizar esta pieza de software sorprendentemente complicada.
published: true
date: 2025-10-05T13:04:29.052Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# 🎛️ 1. Introducción

Por defecto `bredos-news` se inicia cada vez que abras tu shell. Esto está establecido por la línea `bredos-news || true` en `~/.bashrc` y por la existencia de `/etc/profile.d/99-bredos-news.sh`

Cada copia de 'bredos-news' es personalizada, lo que significa que puedes configurar completamente las características que quieres, así como el tema completo.

# 3. Configuración y sobrescritos

Una configuración permenant (por usuario) puede establecerse en `~/.newsrc`. Una configuración en blanco por defecto se genera automáticamente (re)después de la primera ejecución de la aplicación, para que sea posible restablecer su configuración eliminando este archivo.

- El archivo de configuración por defecto debería verse así:

```
"""
Configuración de noticias BredOS-

Consulte `https://wiki.bredos.org/e/en/customizations/news`,
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

El parámetro `Accent` establece los colores primarios, `Accent_Segundo` establece los colores para todos los detalles. Se puede aplicar cualquier secuencia de escape arbitraria ANSI.

> Para más información sobre secuencias de escape ANSI y ejemplos, siga [este enlace](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).
> {.is-info}

Estilos comunes:

| Color            | Código                               |
| ---------------- | ------------------------------------ |
| Púrpura Perfecto | `Acento = "\033[38;5;129m"`         |
|                  | `Accent_Segundo= "\033[38;5;104m"`  |
| Rojo negrita     | `Acento = "\033[1m\033[38;5;124m"` |
|                  | `Accent_Segundo= "\033[38;5;160m"`  |

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
