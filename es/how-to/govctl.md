---
title: Configurando Gobernadores
description: Usando govctl para administrar los gobernadores del sistema
published: true
date: 2025-05-07T12:47:49.03Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.03Z
---

# Usando GovCtl

BredOS envía por defecto la herramienta `govctl` en el paquete `bredos-govctl`.
Está habilitado por defecto y ajustará el rendimiento de acuerdo a la potencia de la batería disponible.

La herramienta establecerá continuamente el gobernador a las configuraciones especificadas, anulaciones u otras herramientas no funcionarán.
Desinstale el paquete si esto es un problema para su flujo de trabajo.

## Comportamiento por defecto

GovCtl asegurará por defecto el máximo rendimiento en todos los dispositivos conectados, si no hay batería interna o el sistema está conectado.

Si el sistema mantiene la carga suficiente, pero no está conectado, mantendrá la mayor parte del rendimiento, limitando la velocidad de la GPU y el impulso de la CPU.

Si el sistema no tiene un cargo suficiente (20% es el punto por defecto en el que se determina esto),
el sistema minimizará el consumo de corriente, en detrimento del rendimiento y del tiempo de respuesta.
Esto por ejemplo hará que los tableros RK3588 sólo funcionen a 300mHz.

Si no le gustan los valores predeterminados, todos pueden ser cambiados.

# Viendo estado del gobernador

Para ver el gobernador aplicado actualmente, simplemente ejecuta `govctl`, el acceso root no es necesario.

```
[bill88t@icu | ~]> govctl

-------------------------------
Gobernador actualmente aplicado: performance
-------------------------------

uso: govctl [-h] [-g {powersave,conservative,performance}]
              [-b {powersave,conservative,performance}] [-e] [-d]
              [-p POWERSAVE_PERCENT]

herramienta de configuración del Gobernador

opciones:
  -h, --help mostrar este mensaje de ayuda y salir de
  -g, --set-gobernador {powersave,conservative,performance}
                        Establecer gobernador deseado
  -b, --set-battery-governor {powersave,conservative,performance}
                        Establecer el gobernador deseado mientras se ejecuta la batería
  -e, --enable-battery-detection
                        Activar detección de estado de batería
  -d, --disable-battery-detection
                        Desactivar detección del estado de la batería
  -p, --powersave-percent POWERSAVE_PERCENT
                        Porcentaje en el que los activadores de power save
```

# Establecer un punto de ahorro de energía diferente

Como indica el menú de ayuda, usando la opción `-p` te permitirá reconfigurar el punto en el que se aplicará `powersave`. Esto es por defecto del 20%, y puede establecerse entre el 1% y el 80%.

Reconfigurar como sigue:

```
sudo govctl -p 30
```

Esto lo pondría en marcha en un 30 %.

# Cambiando el gobernador aplicado

De forma predeterminada, cuando estén disponibles o no baterías, el sistema mantendrá el máximo rendimiento.
Si desea aplicar un perfil de potencia más conservador por ejemplo, ejecute:

```
sudo govctl -g conservador
```

Si en su lugar desea mantener el máximo rendimiento incluso cuando no está conectado, en su lugar ejecutar:

```
rendimiento sudo govctl -b
```

Bandera `-g` establece el gobernador usado cuando se conecta.
Glag `-b` establece el gobernador usado cuando **NOT** conectado.

# Deshabilitando la detección de batería

Deshabilitando la detección de batería con:

```
sudo govctl -d
```

Se asegurará de que en todo momento el gobernador "conectado" se aplique en todo momento.

Para deshacer esto, ejecutar:

```
sudo govctl -e
```