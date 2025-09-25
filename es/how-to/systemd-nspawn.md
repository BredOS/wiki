---
title: Administrar contenedores con systemd-nspawn
description:
published: false
date: 2025-09-25T07:02:39.910Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🎛️ 1. 📥 Instalar el Firmware

`systemd-nspawn` es una herramienta de contenedor ligera que viene con systemd, diseñada para ejecutar un entorno de comandos u sistema operativo en un entorno fuertemente aislado. A menudo descrito como "chroot en esteroides, proporciona una manera conveniente de probar o ejecutar distribuciones completas de Linux o entornos mínimos de una manera segura y controlada.

A diferencia de soluciones de virtualización completas como QEMU o plataformas contenedoras como Docker, `systemd-nspawn` utiliza espacios de nombres y grupos de Linux para crear contenedores con muy poca sobrecarga.

# 3. Crear plantilla de contenedor

Los contenedores que usan nspawn pueden ejecutarse desde cualquier ubicación en tu sistema de archivos, pero la carpeta recomendada es `/var/lib/machines`. Dentro de esta carpeta, creamos una subcarpeta que contiene nuestras raíces Linux/GNU. Para simplificar el proceso, este artículo le guía a través de la creación de una plantilla de contenedor. El contenido de esa carpeta de plantillas puede ser copiado a una nueva ubicación y usado como un nuevo entorno de contenedor.

- Cambiar a raíz:

```
sudo su
```

- Luego cambie el directorio a `/var/lib/machines`:

```
cd /var/lib/máquinas
```

- Y crear una carpeta de plantilla:

```
plantilla mkdir
```

Como un contenedor puede contener cualquier distribución de rootfs, usted es relativamente libre en su elección. Proporcionamos una lista de tarball de distribución mínima, como Debian, Ubuntu y BredOS; Sin embargo, tenga en cuenta que este artículo es específicamente para un contenedor BredOS.

> Cualquier comando que necesite ser ejecutado dentro de su contenedor debe ser ajustado de acuerdo a la variante de su distribución si no está usando BredOS.
> {.is-info}

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) Busque la versión elegida y descargue el .tar.gz para la arquitectura de su CPU.
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) Desplácese hacia abajo y haga clic en la versión que desea descargar, y descargue el .tar.gz para la arquitectura de su CPU.
- [Base de Contenedor de Cálvula](https://fedoraproject.org/misc#minimal) Desplácese hacia abajo y elija entre Base de Contenedores o Base Mínima de Contenedores.
- [Arch Linux](https://archlinux.org/download/) Elige una réplica cerca de ti, luego descarga el archivo .tar.zst .
- [Arch Linux ARM](https://archlinuxarm.org/os/) Descarga el archivo .tar.gz con la etiqueta aarch64 o armv7.
  {.links-list}

Después de haber descargado el tarball rootfs de su elección, tenemos que extraerlo. En este ejemplo hemos descargado el tarball Arch Linux ARM y lo convertimos a BredOS más tarde.

- Todavía como root extrae el tarball en `/var/lib/machines/template`:

```
sudo tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- El contenido de la carpeta `template` debe verse así:

```
ls template/
bin boot dev etc home lib mnt opt proc root run sbin srv sys tmp usr var
```

