---
title: Guía de gestores de paquetes
description: Bienvenido a la guía de Administradores de Paquetes BredOS! Aquí aprenderá cómo instalar y administrar aplicaciones
published: true
date: 2025-09-18T07:23:26.529Z
tags:
editor: markdown
dateCreated: 20/09-20T20:08:39.778Z
---

# 1. Introducción

Bienvenido a la guía de Administradores de Paquetes BredOS! Aquí aprenderá cómo instalar y administrar aplicaciones. ¡Prepárate para tomar el control de las aplicaciones de tu sistema!

# 2. Pacman

Pacman es el gestor de paquetes predeterminado para BredOS, conocido por su velocidad y simplicidad a la hora de administrar paquetes de software.

## 2.1 Cómo instalar paquetes

- Para instalar un paquete con Pacman, utilice el siguiente comando:

```bash
sudo pacman -S <package name>
```

## 2.2 Cómo actualizar el sistema

- Para actualizar todos los paquetes instalados en su sistema, ejecute:

```bash
sudo pacman -Syu
```

Esto sincronizará las bases de datos de paquetes y actualizará todos sus paquetes a sus últimas versiones.

## 2.3 Cómo eliminar paquetes

- Para desinstalar un paquete, use:

```bash
sudo pacman -R <package name>
```

- Si desea eliminar un paquete y sus dependencias no utilizadas, ejecute:

```bash
sudo pacman -Rns <package name>
```

## 2.4 Cómo buscar paquetes

- Para buscar un paquete en los repositorios de Pacman, use:

```bash
pacman -Ss <package name>
```

## 2.5 Comprobar paquetes instalados

- Para listar todos los paquetes instalados, simplemente ejecutar:

```bash
pacman -Q
```

## 2.6 Limpiar caché

- Para limpiar la caché de Pacman y liberar espacio, use:

```bash
sudo pacman -Sc
```

> Pacman es una herramienta esencial para administrar su sistema BredOS, ¡rápido, eficiente y poderoso!
> {.is-success}

# 3. Paco

Flatpak proporciona un entorno sandboiled para ejecutar aplicaciones, independientemente del software del sistema anfitrión.

## 3.1 Cómo instalar Flatpak

- Para instalar Flatpak, ejecute:

```bash
sudo pacman -S flatpak
```

> Puede ser necesario reiniciar su sistema después de instalar Flatpak.
> {.is-info}

## 3.2 Instalar desde Flathub

### 3.2.1 Instalar una aplicación mediante el navegador web

- Vaya a [Flathub](https://flathub.org), encuentre la aplicación que desee y haga clic en instalar.

![flathub-install-button.png](/how-tos/flathub-install-button.png)

### 3.2.2 Instalar una aplicación mediante Terminal

- También puede instalar aplicaciones directamente desde la terminal:

```bash
sudo flatpak install <app name>
```

## 3.3 Desinstalar una aplicación mediante Terminal

- Para eliminar una aplicación, ejecutar:

```bash
sudo flatpak desinstalar <app name>
```

> Alternativamente, puede administrar aplicaciones de Flatpak usando una tienda gráfica como Pamac.
> {.is-info}

# 4. AppImage

AppImage le permite ejecutar aplicaciones como ejecutables independientes sin necesidad de instalación o gestión de paquetes.

## 4.1 Cómo instalar AppImage Launcher

- Para integrar AppImages con su sistema, instale el AppImage Launcher:

```bash
sudo pacman -S appimagelauncher
```

## 4.2 Cómo usar AppImage

- Descargar una AppImage desde la web (por ejemplo, [AppImageUpdate](https://appimage.github.io/AppImageUpdate)).
- Haga doble clic en el archivo AppImage.
- Elige entre **integrar la aplicación en tu sistema** o **ejecutarla una vez**.

> ¡Feliz gestión de paquetes!
> {.is-success}

