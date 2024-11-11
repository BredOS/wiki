---
title: GNOME en el Desafío b
description: null
published: true
date: 2024-11-11T10:39:09.164Z
tags: null
editor: markdown
dateCreated: 2024-10T19:41:06.111Z
---

# Escritorio GNOME en Fy.Ub Dúo

El escritorio gnome-se puede instalar con el paquete `gnome-meta`.

---

Para una operación adecuada también debería cambiar a GDM después de la instalación. Esto se puede hacer ejecutando:

```
sudo systemctl deshabilita lightdm
sudo systemctl habilitar gdm
```

Sólo el wayland de Gnome está soportado.

## Fijar rotación de pantalla

**Si** en tu ARCHIVO la pantalla gira incorrectamente, necesitas instalar y configurar la extensión `Rotar pantalla`.

### 1. Instalar gestor de extensiones

Ejecuta `sudo pacman -S extension-manager` para instalarlo, y abre la aplicación.

### 2. Instalar rotación de pantalla

Después de abrir la aplicación, pulsa `Examinar` > `Buscar` > Escribe `Rotar pantalla` > Instala `Rotar pantalla` por `shyzus`.

### 3. Configurar rotación de pantalla

Vaya de vuelta a la página 'Instalado' del Administrador de extensiones y pulse la rueda dentada de ajustes para abrir el panel de ajustes de la extensión.
Entonces deberías aumentar el valor de `Establecer desplazamiento de orientación` a 1.

## Uso del paisaje plano de uso

El estilo sólo apuntará correctamente cuando la pantalla se rote verticalmente de forma predeterminada.
Para establecer esto en su lugar trabajar horizontalmente:

### 1. Abre `mañ/udev/rules.d/fydetab.rules`

Para abrir el archivo, ejecutar:

```
sudo nano ► /udev/rules.d/fydetab.rules
```

### 2. Añadir la línea de configuración

En la parte inferior del archivo, agregar:

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 0 0 0 0 1"
```

### 3. Reboot

Después de reiniciar el lápiz funcionará correctamente.

Si intentaste con error la calibración de la configuración de gnome, elimina los datos de calibración ejecutando:

```
reset dconf -f /org/gnome/desktop/peripherals/tablets
```
