---
title: Guía de personalización de BredOS Shell
description: ¡Esta guía te ayudará a personalizar tu experiencia BredOS cambiando y mejorando tu shell!
published: true
date: 2025-09-16T10:37:25.923Z
tags: personalización, shell
editor: markdown
dateCreated: 2024-20-20T19:39:08.509Z
---

# 1. Introducción

¡Esta guía te ayudará a personalizar tu experiencia BredOS cambiando y mejorando tu shell!  Tanto si prefiere Bash, Zsh, Fish o Nushell, encontrará todo lo que necesita aquí. ¡Vamos a bucear!

# 2. Bash

> Bash es el shell predeterminado en BredOS.
> {.is-info}

## 2.1 Instalar Bash

- Para instalar Bash, ejecutar:

```bash
sudo pacman -S bash
```

## 2.2 Establecer Bash como Shell predeterminado

- Para listar todos los shells instalados, ejecute:

```bash
   chsh -l
```

- Para establecer Bash como su shell predeterminado:

```bash
   chsh -s /usr/bin/bash
```

Cerrar sesión y volver a iniciar sesión para comenzar a usar Bash como su shell.

## 2.3 Oh Mi Bash

¡Mejora Bash con **Oh My Bash**, un framework que añade temas, plugins y otras mejoras geniales!

# 3. Zsh

Zsh es un potente shell con muchas características avanzadas que lo hacen más versátil que Bash.

## 3.1 Install Zsh

- Para instalar Zsh, ejecute:

```bash
sudo pacman -S zsh
```

## 3.2 Características

- **Mejor finalización de tabulación**: Zsh solo muestra destinos válidos cuando se usan comandos como `cd`.
- **Mejor búsqueda de historiales**: Escribe parte de un comando anterior y presiona ⬆️ para buscar a través de tu historial.

## 3.3 Establecer Zsh como Shell predeterminado

- Para listar todos los shells instalados, ejecute:

```bash
   chsh -l
```

- Para establecer Zsh como su shell predeterminado:

```bash
   chsh -s /usr/bin/zsh
```

¡Cerrar sesión y volver a iniciar sesión para cambiar a Zsh!

## 3.4 Oh Mi Zsh

**Oh My Zsh** es un framework impulsado por la comunidad que mejora Zsh con temas y plugins, dándote aún más energía y flexibilidad.

# 4. Pescado

El **Fish** (concha interactiva amigable) se centra en la facilidad de uso y viene con excelentes características.

## 4.1 Instalar pescado

- Para instalar Fish, ejecute:

```bash
sudo pacman -S fish
```

## 4.2 Características

- **Autosuggestions**: Fish sugiere comandos a medida que escribes, basados en tu historia.
- **Configuración basada en la Web**: Personaliza la apariencia y el comportamiento de tu shell a través de una interfaz web.
- \*\*Funciona fuera de la caja \*\*: Finalización de la tabulación, resaltado de sintaxis, ¡y más sin ninguna configuración adicional!

## 4.3 Establecer pescado como proyectil predeterminado

- Para listar todos los shells instalados, ejecute:

```bash
   chsh -l
```

- Para establecer el pescado como su concha predeterminada:

```bash
   chsh -s /usr/bin/fish
```

¡Salga y vuelva a iniciar sesión para disfrutar de Fish!

## 4.4 Oh Mi Peces

Usa **Oh My Fish** para añadir plugins y temas a Fish, mejorando su funcionalidad y estética.

# 5. Nusillo

**Nushell** adopta un enfoque moderno para el scripting de shell, tratando toda la entrada como datos estructurados, facilitando su manejo.

## 5.1 Instalar Nushell

- Para instalar Nushell, ejecute:

```bash
sudo pacman -S nushell
```

## 5,2 Características

- **Todo es datos**: Los pipelines Nu manejan datos estructurados para filtrar, ordenar y seleccionar fácilmente.
- **Plugins potentes**: Extiende fácilmente Nushell con una amplia gama de plugins.
- **Buen mensaje de error**: Nushell te ayuda a detectar errores temprano con mensajes de error útiles.

## 5.3 Establecer Nushell como Predeterminado Shell

- Para listar todos los shells instalados, ejecute:

```bash
   chsh -l
```

- Para establecer Nushell como su shell predeterminado:

```bash
   chsh -s /usr/bin/nu
```

¡Cerrar sesión y volver a iniciar sesión para cambiar a Nushell!
