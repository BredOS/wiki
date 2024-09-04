---
title: Guía de instalación para BredOS
description: null
published: true
date: 2024-16T10:06:04.691Z
tags: null
editor: markdown
dateCreated: 2024-19T00:42:37.505Z
---

# 🍞 Guía de instalación de BredOS

## 📚 Tabla de contenidos

- [🔽 Descargando BredOS](#downloading-bredos)
- [💽 Creando el medio de instalación (microSD)](#creating-the-installation-media-microsd)
- [🚀 Arranque desde el medio de instalación (microSD)](#booting-from-the-installation-media-microsd)
- [💾 Instalar BredOS a eMMC (RockChip)](#installing-bredos-to-emmc-rockchip)
- [💻 Sigue al instalador BredOS](#follow-bredos-installer)
- [🛠️ Configuración inicial](#initial-configuration)

## 🔽 Descargando BredOS

Descarga la última imagen de BredOS para tu consola desde el [🌐 sitio web oficial](https://bredos.org/download.html).

## 💽 Creando el medio de instalación (microSD)

1. Inserta tu tarjeta microSD en tu ordenador.
2. Usa una herramienta como [`balenaEtcher`](https://etcher.balena.io/), `dd`, o [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) para escribir la imagen BredOS en la tarjeta microSD.

## 🚀 Arranque desde el medio de instalación (microSD)

1. Inserte la tarjeta microSD en el ordenador de una sola placa ARM.
2. Conecte los periféricos necesarios (teclado, ratón, monitor) y encendido en el dispositivo.
3. El dispositivo debería arrancar desde la tarjeta microSD y cargar el instalador BredOS.

## 💾 Instalar BredOS a eMMC (RockChip)

Si quieres instalar BredOS en el almacenamiento eMMC en lugar de usar una tarjeta microSD, sigue estos pasos:

**📝 Antes de comenzar, asegúrate de tener los siguientes archivos descargados:**

- [📥 Rockchip Driver](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip)

- Herramienta de flasheo **(RKDevTool vX.XX)**: Puede descargar las herramientas para Windows en los siguientes enlaces:
  - [🔗 Enlace 1](https://docs.radxa.com/es/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)
  - [🔗 Alternativo en caso de que `Link 1` no funcione](https://dl.radxa.com/tools/windows/)
  - [🔗 Enlace a la versión v2.96](https://dl.radxa.com/tools/windows/RKDevTool_Release_v2.96_zh.zip)

- Archivo de cargador SPI, por ejemplo para el RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

- [Imagen BredOS](#downloading-bredos).

\*\*📂 Descomprima todos los archivos incluyendo la imagen BredOS, que por defecto viene en un .

- Lo primero que hay que hacer es instalar el controlador Rockchip que hemos descargado. Para esto, abre la carpeta `DriverAssitant_v5.0` y ejecuta el archivo `DriverInstall.exe`.

- Haga clic en `🟢 Instalar Driver`:

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Android/AOSP/install_drivers.png)

- Abre la carpeta que contiene la herramienta de flasheo: carpeta `RKDevTool_Release_v2.96` (comprueba la versión que has descargado para el nombre) y ejecuta la herramienta `RKDevTool.exe`.

- En la herramienta de flasheo establezca la siguiente configuración y haga clic en `RUN`:
  - Seleccione el archivo de cargador SPI
  - Seleccione la imagen BredOS
  - Comprueba `Escribir por Dirección`
  - Haga clic en `RUN` y espere hasta que el proceso termine

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/flashing_tool_config.png)

## 💻 Sigue el instalador de BredOS

1. Siga las instrucciones en pantalla para completar el proceso de instalación.
2. Seleccione su idioma preferido, disposición del teclado y zona horaria.
3. Configurar una cuenta de usuario y contraseña.
4. Completa la instalación y reinicia el dispositivo.

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/bredOS_installer.jpg)

## 🛠️ Configuración inicial

Después de ejecutar el instalador BredOS puede que necesite completar algunas tareas iniciales de configuración:

- 🌐 Configurar ajustes de red
- 🔄 Actualizar el sistema usando el gestor de paquetes
- 🛠️ Instalar paquetes de software adicionales según sea necesario

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)
