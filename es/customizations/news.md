---
title: Noticias BredOS
description: Personalizar esta pieza de software sorprendentemente complicada.
published: true
date: 2025-10-04T21:14:51.210Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# Introducción

BredOS News se inicia cada vez que abre su shell.

BredOS por defecto configura `~/.bashrc` y `/etc/profile.d/99-bredos-news.sh` para ejecutarlo por defecto.

Cada copia de las noticias es personalizada.

Puedes configurar completamente las características que quieras, así como el tema completamente.

## Configuración y sobrescritos

BredOS News ofrece bastantes maneras de personalizarlo.
La configuración permenante (por usuario) se puede hacer en `~/.newsrc`.

La configuración en blanco por defecto se genera automáticamente (re)después de la primera ejecución de la aplicación.
El archivo por defecto se ve así en el momento de escribir:

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

`Accent` establece los colores principales, `Accent_Segundo` establece los colores para todos los detalles.
Se puede aplicar cualquier secuencia de escape arbitraria ANSI.
Para más información sobre secuencias de escape ANSI y ejemplos, siga [este enlace](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797).

### Deshabilitando características

`.h_Updates` elimina completamente la sección de actualizaciones del paquete.
`.h_Disks` elimina las notas de uso de almacenamiento medio adjunto.
`.h_Smart` silencia las advertencias de fallo del disco. Esto NO debe ser utilizado.

### Configurando tiempo de animación

`Time_Tick` configura el tiempo entre fotogramas de la animación.
`Time_Refresh` configura con qué frecuencia se actualizan los detalles del sistema.
Estos valores son los mejores ya existentes. No reduzca más o el uso de cpu **será** ppike.

`Onetime` desactiva el bucle de animación, el sistema de acceso directo y las funciones de redimensionamiento de la terminal.

## Atajos

`shortcuts` es un diccionario de keybinds configurables. Rick-dial para su terminal.

Mientras que News está haciendo bucle en su animación, pulsando una de las teclas configuradas, en lugar de pasar la tecla al intérprete, se iniciará el atajo preconfigurado.

Configurar teclas, como se muestra en el ejemplo, permite ejecutar comandos o funciones de python.
Las operaciones de shell, como cambiar directorio y/o tuberías están totalmente soportadas.
Las claves especiales y combinaciones no están soportadas actualmente.
Los Symbols son compatibles.

## Sobreescritura del entorno

Establecer `HUSH_NEWS=1` evitará que BredOS News se ejecute.

Crear `~/.hush_login` también tiene el mismo efecto.