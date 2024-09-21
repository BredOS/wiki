---
title: Guía de personalización de BredOS Shell 🐚🎨
description: ¡Esta guía te ayudará a personalizar tu experiencia BredOS cambiando y mejorando tu shell! 🚀 Si prefieres Bash, Zsh, Fish o Nushell, encontrarás todo lo que necesitas aquí. ¡Vamos a bucear! 🌊
published: true
date: 2024-09-21T09:02:20.084Z
tags: personalización, shell
editor: markdown
dateCreated: 2024-20-20T19:39:08.509Z
---

# Guía de personalización de BredOS Shell 🐚🎨

¡Esta guía te ayudará a personalizar tu experiencia BredOS cambiando y mejorando tu shell! 🚀 Si prefieres Bash, Zsh, Fish o Nushell, encontrarás todo lo que necesitas aquí. ¡Vamos a bucear! 🌊

---

## 📚 Índice de contenidos

- Bash 🐢
- Zsh ⚡
- Pez :púpico_pez:
- Nushell 🧠

---

## Bash 🐢

Bash es el shell predeterminado en BredOS. ¡Empecemos con configurarlo o haciéndolo su shell predeterminado!

### Instalar Bash 🛠️

Para instalar Bash, ejecutar:

```bash
sudo pacman -S bash
```

### Establecer Bash como predeterminado ⚙️

1. Para listar todos los shells instalados, ejecute:
   ```bash
   chsh -l
   ```
2. Para establecer Bash como su shell predeterminado:
   ```bash
   chsh -s /usr/bin/bash
   ```
3. Cerrar sesión y volver a iniciar sesión para comenzar a usar Bash como su shell. 🔄

### Oh Mi Bash 💡

¡Mejora Bash con **Oh My Bash**, un framework que añade temas, plugins y otras mejoras geniales! 🌟

---

## Zsh ⚡

Zsh es un potente shell con muchas características avanzadas que lo hacen más versátil que Bash.

### Instalar Zsh 🛠️

Para instalar Zsh, ejecute:

```bash
sudo pacman -S zsh
```

### Características 🌟

- \*\*Mejor finalización de la pestaña \*\* ⌨️: Zsh muestra sólo destinos válidos cuando se utilizan comandos como `cd`.
- **Mejor búsqueda de historial** 🔍: Escribe parte de un comando anterior y presiona ⬆️ para buscar a través de tu historial.

### Oh Mi Zsh 🧩

**Oh My Zsh** es un framework impulsado por la comunidad que mejora Zsh con temas y plugins, dándote aún más energía y flexibilidad. ✨

### Establecer Zsh como Shell ⚙️

1. Para listar todos los shells instalados, ejecute:
   ```bash
   chsh -l
   ```
2. Para establecer Zsh como su shell predeterminado:
   ```bash
   chsh -s /usr/bin/zsh
   ```
3. ¡Cerrar sesión y volver a iniciar sesión para cambiar a Zsh! 🔄

---

## Pez :púpico_pez:

El **Fish** (concha interactiva amigable) se centra en la facilidad de uso y viene con excelentes características.

### Instalar Fish 🛠️

Para instalar Fish, ejecute:

```bash
sudo pacman -S fish
```

### Características 🌟

- **Autosuggestions** 🤖: Fish sugiere comandos a medida que escribes, basados en tu historial.
- **Configuración basada en la Web** 🌐: Personaliza la apariencia y el comportamiento de tu shell a través de una interfaz web.
- \*\*Funciona fuera de la caja \*\* 🧰: Finalización de tabulación, resaltado de sintaxis, ¡y más sin ninguna configuración adicional!

### Oh My Fish 🎣

Usa **Oh My Fish** para añadir plugins y temas a Fish, mejorando su funcionalidad y estética. 🌈

### Establecer pescado como concha predeterminada ⚙️

1. Para listar todos los shells instalados, ejecute:
   ```bash
   chsh -l
   ```
2. Para establecer el pescado como su concha predeterminada:
   ```bash
   chsh -s /usr/bin/fish
   ```
3. ¡Salga y vuelva a iniciar sesión para disfrutar de Fish! 🔄

---

## Nushell 🧠

**Nushell** adopta un enfoque moderno para el scripting de shell, tratando toda la entrada como datos estructurados, facilitando su manejo.

### Instalar Nushell 🛠️

Para instalar Nushell, ejecute:

```bash
sudo pacman -S nushell
```

### Características 🌟

- **Todo es datos** 📊: Los pipelines Nu manejan datos estructurados para facilitar el filtro, ordenar y seleccionar.
- **Plugins potentes** 🔌: Extender fácilmente Nushell con una amplia gama de plugins.
- **Buen mensaje de error** 🛠️: Nushell te ayuda a detectar errores temprano con mensajes de error útiles.

### Establecer Nushell como Shell predeterminado ⚙️

1. Para listar todos los shells instalados, ejecute:
   ```bash
   chsh -l
   ```
2. Para establecer Nushell como su shell predeterminado:
   ```bash
   chsh -s /usr/bin/nu
   ```
3. ¡Cerrar sesión y volver a iniciar sesión para cambiar a Nushell! 🔄
