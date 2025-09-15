---
title: Configurando Gobernadores
description: Usando govctl para administrar los gobernadores del sistema
published: true
date: 2025-09-15T09:02:10.135Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.03Z
---

# 1. Introducción

BredOS envía por defecto la herramienta `govctl` en el paquete `bredos-govctl`.
Está habilitado por defecto y ajustará el rendimiento de acuerdo a la potencia de la batería disponible.

- Esto debe ser instalado por defecto. Si no, instálalo con

```
sudo pacman -S bredos-govctl
```

La herramienta establecerá continuamente el gobernador a las configuraciones especificadas, anulaciones u otras herramientas no funcionarán.

- Desinstale el paquete si esto es un problema para su flujo de trabajo.

```
sudo pacman -R bredos-govctl
```

## 1.1 Comportamiento por defecto

GovCtl asegurará por defecto el máximo rendimiento en todos los dispositivos conectados, si no hay batería interna o el sistema está conectado.

Si el sistema mantiene la carga suficiente, pero no está conectado, mantendrá la mayor parte del rendimiento, limitando la velocidad de la GPU y el impulso de la CPU.

Si el sistema no tiene un cargo suficiente (20% es el punto por defecto en el que se determina esto),
el sistema minimizará el consumo de corriente, en detrimento del rendimiento y del tiempo de respuesta.
Esto por ejemplo hará que los tableros RK3588 sólo funcionen a 300mHz.

Si no le gustan los valores predeterminados, todos pueden ser cambiados.

## 1.2 Ver estado del gobernador

- Para ver el gobernador aplicado actualmente, simplemente ejecuta `govctl`, el acceso root no es necesario.

```
govctl
```

```
-------------------------------
Gobernador aplicado actualmente: performance
-------------------------------

usage: govctl [-h] [-g {powersave,conservative,performance}]
              [-b {powersave,conservative,performance}] [-e] [-d]
              [-p POWERSAVE_PERCENT]

Herramienta de configuración del Gobernador

opciones:
  -h, --help mostrar este mensaje de ayuda y salir de
  -g, --set-gobernador {powersave,conservative,performance}
                        Establecer gobernador deseado
  -b, --set-battery-governor {powersave,conservative,performance}
                        Establecer gobernador deseado mientras se ejecuta la batería
  -e, --enable-battery-detection
                        Activar detección de estado de batería
  -d, --disable-battery-detection
                        Desactivar detección del estado de la batería
  -p, --powersave-percent POWERSAVE_PERCENT
                        Porcentaje en el que los activadores de power save
```

## 1.3 Establecer un punto de ahorro de energía diferente

Como indica el menú de ayuda, usando la opción `-p` te permitirá reconfigurar el punto en el que se aplicará el gobernador `powersave`. Por defecto, esto es del 20%, y puede establecerse entre el 1% y el 80%.

- Reconfigurar como sigue:

```
sudo govctl -p 30
```

Esto lo pondría en marcha en un 30 %.

## 1.4 Cambiando el gobernador aplicado

De forma predeterminada, cuando estén disponibles o no baterías, el sistema mantendrá el máximo rendimiento.

- La bandera `-g` establece el gobernador usado cuando se conecta. Si quieres que sea `conservador` mientras tu sistema se está apagando de energía:

```
sudo govctl -g conservador
```

- La bandera `-b` establece el gobernador usado cuando **NOT** conectado. Si quieres que sea `performance` mientras tu sistema se está ejecutando sin batería:

```
rendimiento sudo govctl -b
```

## 1.5 Deshabilitando la detección de batería

- Deshabilitando la detección de batería con:

```
sudo govctl -d
```

Se asegurará de que en todo momento el gobernador "conectado" se aplique en todo momento.

- Para deshacer esto, ejecutar:

```
sudo govctl -e
```