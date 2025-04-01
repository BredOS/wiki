---
title: Página web
description: null
published: true
date: 2024-09-04T12:54:13.878Z
tags: null
editor: markdown
dateCreated: 2022-08-24T12:37:36.410Z
---

# 🍞 La Wiki de BredOS

## 🌟 Resumen

¡Bienvenido a la documentación de BredOS! BredOS es una distribución de Linux basada en Ark específicamente diseñada para ordenadores de una sola placa (SBCs) basados en ARM.
La documentación le guiará a través de la instalación, configuración y uso de BredOS.

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

## 📚 Índice de contenidos

1. [🔍 Introducción](#introduction)
2. [🚀 Características](#features)
3. [🛠️ Requisitos del sistema](#requisitos del sistema)
4. [💽 Instalación](/installation)
5. [📦 Administración de Paquetes](#package-management)
6. [🐞 Resolución de problemas](#troubleshooting)
7. [❓FAQ](#faq)
8. [🌐 Comunidad y soporte](#community-and-support)
9. [🤝 Contributando](#contributing)

## 🔍 Introducción

BredOS tiene como objetivo proporcionar una experiencia fácil y amigable para los usuarios de computadoras de una sola tarjeta basada en ARM. Aprovechando el poder y la flexibilidad de Arch Linux, BredOS ofrece una plataforma robusta que puede adaptarse a una amplia gama de casos de uso.

## 🚀 Características

- **🖥️ Interfaz amigable con el usuario**: Una interfaz de usuario simplificada e intuitiva para una fácil navegación y uso.
- **🎯 Arch-Based**: Construido sobre Arch Linux, asegurando el acceso a un vasto repositorio de paquetes y a un modelo de lanzamiento rodante.
- **🔧 Soporte ARM**: Optimizado para computadoras de una sola placa basadas en ARM, haciéndolo ideal para dispositivos como la Rock 5B, y más.
- **⚡ Lightweight**: Mínima inflación, asegurando un sistema ligero y receptivo.

## 🛠️ Requisitos del sistema

- **🖥️ Dispositivos soportados**:
  - Roca de Radxa 5 A/B/C
  - Roca Radxa 4 C
  - Kit Radxa NX5
  - Nova IndieDroid
  - Pi Naranja 5/5+
  - Borde Khadas 2
  - Khadas VIM 4
  - Pi Pi 4B
  - [Dúo de Fya](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/blob/main/Documentation/Linux_distros/bredos.md)
- **🧠 RAM mínimo**: 2 GB
- **💾 Almacenamiento**: tarjeta microSD de 16 GB o mayor
- **🌐 Red**: Opcional

## 💽 Instalación

Lee más en nuestra [Guía de instalación](/installation).

## 📦 Gestión de paquetes

BredOS usa `pacman`, el gestor de paquetes de Arch Linux. Aquí hay algunos comandos comunes:

- 🔄 Actualizar lista de paquetes: `sudo pacman -Syu`
- ➕ Install a package: `sudo pacman -S [package_name]`
- ➖ Eliminar un paquete: `sudo pacman -R [package_name]`
- 🔍 Busca un paquete: `pacman -Ss [package_name]`

## 🐞 Solución de problemas

Si encuentras problemas con BredOS, serás bienvenido a unirte a nuestra [discord](https://discord.gg/jwhxuyKXaa).

## ❓ FAQ

### ❓ Q: ¿Qué dispositivos soportan BredOS?

R: BredOS soporta una variedad de computadoras de una sola placa basadas en ARM, la lista completa está disponible en [dispositivos compatibles](#system-requirements).

### 🔄 Q: ¿Cómo actualizo BredOS?

R: Puedes actualizar BredOS usando el gestor de paquetes `pacman` con el comando `sudo pacman -Syu`.

### 📦 Q: ¿Dónde puedo encontrar paquetes de software adicionales?

R: Puede encontrar paquetes de software adicionales en el repositorio de usuarios de Arch (AUR) e instalarlos usando `yay` o `paru`.

### P: El consumo de energía de mi dispositivo es alto, ¿cómo puedo reducirlo?

R: Usted puede reducir el consumo de energía cambiando el gobernador de CPU a 'ondemand' o 'conservador' editando el archivo de 'is/default/cpupower'.

### P: La suspensión no funciona.

R: Por favor, asegúrese de que:

- No suspenda antes de las 10 después de reanudarse, este es un problema conocido con el controlador eMMC.
- ¡No configure "suspender" como la acción del botón de encendido, porque suspenderá el dispositivo inmediatamente después de reanudar! (¡Esto hará que el dispositivo introduzca un bucle de suspensión de reanudación!)

## 🌐 Comunidad y soporte

Únete a la comunidad BredOS para obtener apoyo, compartir ideas y contribuir al proyecto:

- [📱 Telegram](https://t.me/bredoslinux)
- [:speech _balloon: Discord](https://discord.gg/jwhxuyKXaa)
- [💻 GitHub](http://github.com/BredOS)

## 🤝 Contribuyendo

BredOS es un proyecto de código abierto, y las contribuciones son bienvenidas! Puedes contribuir de las siguientes maneras:

- 🐛 Reportar errores y problemas
- 💻 Enviar parches y mejoras
- 📄 Escribe y mejora la documentación
- :peopleple_holding_hands: Ayuda a otros usuarios en los foros de la comunidad y chatea

Para más información sobre contribuir, visita [💻 GitHub](http://github.com/BredOS) o puedes enviarnos un mensaje en [:speech _balloon: Discord](https://discord.gg/jwhxuyKXaa) o unirte a nuestro [📱 Telegram](https://t.me/bredoslinux).
