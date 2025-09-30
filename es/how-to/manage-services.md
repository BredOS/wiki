---
title: Cómo administrar los servicios
description:
published: false
date: 2025-09-30T11:18:31.209Z
tags:
editor: markdown
dateCreated: 2025-09-30T10:31:51.284Z
---

# 🎛️ 1. 📥 Instalar el Firmware

La gestión de servicios es una parte central de la administración de un sistema Linux, y systemctl—parte de la suite systemd—es la herramienta principal para el trabajo en la mayoría de las distribuciones modernas, incluyendo BredOS. Si necesita iniciar un servicio, detenerlo, compruebe su estado. o configurarlo para que se ejecute al arranque, systemctl proporciona una interfaz consistente y potente. Esta guía le guiará a través de los comandos esenciales y ejemplos prácticos para ayudarle a tomar el control de los servicios del sistema con confianza.

# 3. Examine sus servicios

## 2.1 Con `bredos-news`

- La herramienta `bredos-news` se inicia automáticamente cuando se abre la línea de comandos.

![bredos-news.png](/systemd/bredos-news.png)

Al final de su salida, puede leer el texto "El sistema funciona normalmente". Esto significa que todos los servicios que se supone que se inician en el arranque han sido iniciados sin ningún error. Si acaba de iniciar su dispositivo, puede mostrar la advertencia "AÑADIR AÑADIR AQUÍ". Esto es normal, ya que muchos servicios pueden iniciarse en paralelo, lo que puede provocar retrasos al iniciar. Esta advertencia debería desaparecer después de unos minutos.

Si ves el mensaje de error, "POR FAVOR AÑADIR ERROR MESSAGE HERE", uno o más servicios no han podido iniciarse. Para identificar el problema con el servicio y potencialmente arreglarlo, continúe con la Sección 3.

## 2.2 Con `systemctl`

- Para listar todos los servicios en su computadora ejecute:

```
systemctl list-units --type=service
```

Esto genera una lista de servicios. Navega con tus teclas de flecha, o usa <kbd>espacio</kbd> para ir una página abajo. Déjalo con la tecla <kbd>Q</kbd>.

Los servicios pueden tener diferentes estados como se muestra en la fila "SUB". Pueden ser `running`, `exited`, o `failed`.

- Un servicio `corriendo` realiza tareas de fondo para ti. Un buen ejemplo de esto es Network Manager. Este servicio administra la conectividad de red. Ya que siempre se puede conectar un cable Ethernet, el programa debe ejecutarse continuamente para gestionar la red en consecuencia. Esto se consigue mediante un servicio `ejecutando`.

- Un servicio `exited` es uno que se ejecuta al arrancar, realiza su tarea y luego termina limpiamente. Un buen ejemplo de esto es el servicio systemd-tmpfiles-configuración. Comienza al arrancar, monta un ramdisk, lo monta a /tmp, y luego sale con gracia.

- Un servicio `failed` no se inició correctamente o se encontró con un problema mientras se ejecutaba y se detuvo con un código de error. Esto no significa que su sistema esté dañado, pero corregirlo podría ser recomendable.

También es posible comprobar el estado de un servicio dado, que proporciona más salida, incluyendo su mensaje de error, si ha fallado.

- Para comprobar el estado de un servicio dado ejecutar:

```
estado de systemctl <your service name here>
```

- Por ejemplo, aquí está la salida de un servicio fallido que contiene su problema:

```
● nordvpnd.service - NordVPN Daemon
     Cargado: cargado (/usr/lib/systemd/system/nordvpnd. ervice; enabled; preset: disabled)
     Active: activating (auto-restart) (Result: exit-code) since Fri 2025-09-26 12:53:07 CEST; Hace 3s
 Invocación: adf87be78f8b44e3ba66a18268b87241
TriggeredBy: ● nordvpnd. ocket
    Proceso: 1916 ExecStart=/usr/sbin/nordvpnd (code=exited, status=127)
   PID principal: 1916 (code=exitado, status=127)
   Mem piak: 2M
        CPU: 28ms

Sep 26 12:53:13 bredos systemd[1]: nordvpnd. ervice: Reinicio programado de trabajo, contador de reinicio está en 1.
Sep 26 12:53:13 bredos systemd[1]: Detenido NordVPN Daemon.
Sep 26 12:53:13 bredos systemd[1]: NordVPN Daemon iniciado.
Sep 26 12:53:13 bredos nordvpnd[1971]: /usr/sbin/nordvpnd: error al cargar librerías compartidas: libxml2. o.2: cannot open shared object file: no such file or directory
Sep 26 12:53:13 bredos systemd[1]: nordvpnd. ervice: Proceso principal terminado, code=exited, status=127/n/a
Sep 26 12:53:13 bredos systemd[1]: nordvpnd.service: Error con resultado 'exit-code'.
```

En el ejemplo anterior, el servicio nordvpnd no pudo iniciarse porque le falta la librería libxml2.so.2. Con esta información, es fácilmente fijable.

# 4. Administrar servicios

Los servicios pueden iniciarse y/o detenerse manualmente o al arrancar. Para gestionar el comportamiento de un servicio hacer lo siguiente.

- Para iniciar un servicio manualmente, ejecute:

```
sudo systemctl iniciar <your service name here>
```

- Y para detenerlo, ejecutar:

```
sudo systemctl stop <your service name here>
```

La lógica continúa con la activación y desactivación de servicios al arrancar. Usa `systemctl enable` para iniciarlos al arrancar, o `systemctl disable` para evitar que inicien al arrancar. Con el parámetro `--now`, puede iniciarlos y activarlos al mismo tiempo.

- Por ejemplo, si quieres activar nordvpnd en el arranque y iniciarlo con el mismo comando, ejecutar:

```
sudo systemctl habilitar --now nordvpnd
```
