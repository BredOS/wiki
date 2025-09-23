---
title: Wiki de BredOS
description:
published: false
date: 2025-09-23T09:15:42.581Z
tags:
editor: markdown
dateCreated: 2025-09-19T15:05:44.344Z
---

# 1. Resumen

¡Bienvenido a la documentación de BredOS! La documentación le guiará a través de la instalación, configuración y uso de BredOS.
La documentación le guiará a través de la instalación, configuración y uso de BredOS.

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

# 2. Características

- Hecho con pasión - sólo para su disfrute!
- ¡Soporte al usuario con gran respeto! No importa si usted es un poco de migajas o todo un plano!
- ¡Simple y simple por diseño! ¡Sin problemas, garantizando un sistema ligero y receptivo!
- Arquero - con personalización hecha a medida para ser pulida y fácil de usar.

## 2.1 Herramientas destacadas

- Pastelería - [tu guía para tu propio Bred](/install/first-setup)!
- Bred-Tools - [el cuchillo suizo a tu mano](/Tools)!
- Bred-Config - [como raspi-config, ¡pero con mejor gusto!](/bredos-config)
- Govctl - [toma el control de tu CPU](/how-to/govctl)!

# 3. Requisitos del sistema

Soportamos una amplia gama de dispositivos: desde emocionantes sistemas basados en ARM y configuraciones experimentales RISC-V hasta viejos paneles de intel/amd x86. Lo tenemos cubierto, si usas nuestra [línea principal . así instalación](/en/install/Installation-with-ISO) o consulte la lista de dispositivos que soportamos pasivamente en nuestra [tabla de dispositivos compatibles](/en/table-of-supported-devices).

## 3.1 Requisitos mínimos del sistema

- RAM mínimo: 2 GB
- Storage: 8 GB microSD card or larger

# 4. Instalación

Nuestro amigo **DroidMaster** hizo un video de YouTube sobre BredOS. Échale un vistazo aquí:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/eoLE27xdtu4?si=ai-0QqLNyCYfTKfA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# 5. Instalación

To make installation easy for you, we laid out a line of bred crumbs to follow. 🍞 🔸🔸🔸

> Si encontraste un trozo de pan 🔸 danos una cabecera en nuestros canales comunitarios.
> {.is-info}

## 5.1 Instalación de imagen específica del dispositivo

Estos son los tableros que más nos gustan. Para instalar estas imágenes BredOS en ellas, inicia con nuestra [imagen específica del dispositivo](/install/device-specific-image) guía de instalación, o dar un vistazo a la página del dispositivo en nuestra wiki, que se puede encontrar en la barra de navegación a la izquierda de esto.

Visita nuestro [sitio de descargas](https://bredos.org/download.html) para averiguar si tu dispositivo es uno de ellos.

## 12.2 Instalación genérica

Si tu dispositivo no aparece en nuestro [sitio de descargas](https://bredos.org/download.html) pero soporta el arranque de UEFI y se basa en la arquitectura x86 o ARM64, simplemente sigue nuestra guía para una instalación genérica disponible [here](/install/Installation-with-ISO).

## 5.3 Instalación del contenedor Docker

- Fácil como una línea de comando:

```
trituradores/bredos/bredos
```

# 5. Solución de problemas

Eche un vistazo a las páginas del dispositivo en la barra de navegación de esta página para encontrar problemas conocidos específicos de su dispositivo. Si tu problema no está listado, no dudes en contactar con nosotros directamente a través de [nuestros canales de soporte](#h-7-community-and-support).

# 4. Comunidad y soporte

Únete a la comunidad BredOS para obtener apoyo, compartir ideas y contribuir al proyecto:

- [Telegram](https://t.me/bredoslinux)
- [Discord](https://discord.gg/jwhxuyKXaa)
- [GitHub](http://github.com/BredOS)

# 8. Contribuyendo

BredOS es un proyecto de código abierto, y las contribuciones son bienvenidas! Puedes contribuir de las siguientes maneras:

- Reportar errores y problemas
- Enviar parches y mejoras
- Escriba y mejore la documentación
- Ayuda a otros usuarios en los foros de la comunidad y chatea

# 9. Campaña principal

Ahora mismo, las imágenes BredOS para dispositivos RK3588 dependen del crusty Rockchip BSP kernel — un abrazo, código codificado con ductos que es difícil de mantener, inseguro y siempre señala detrás de Linux.

[Queremos cambiar eso](/en/internal-bred-stuff/mainline-campaign).
