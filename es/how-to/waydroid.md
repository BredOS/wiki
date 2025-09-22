---
title: Ejecutar aplicaciones Android (waydroid)
description:
published: true
date: 2025-09-21T12:54:43.353Z
tags:
editor: markdown
dateCreated: 2025-09-21T08:40:19.752Z
---

# 1. Introducción

Waydroid es una solución basada en contenedores para ejecutar Android en Linux/GNU usando Wayland. Esta guía le guiará a través de los pasos necesarios para instalarlo.

# 2. Instalación

- Install Waydroid:

```
sudo pacman -S waydroid
```

## 2.1 RK3588

Necesitas activar el panthor y configurar sigue [esta guía](/how-to/how-to-setup-panthor).

- Install panthor image:

```
sudo pacman -S waydroid-panthor-image
```

- Initialize waydroid:

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

## 2.2 ARM64/X86_64 genéricos

- Esto descargará e instalará la versión GAPPS de android:

```
sudo waydroid init -s GAPPS
```

# 3. Activar e iniciar waydroid

- Activar e iniciar Waydroid:

```
sudo systemctl habilitar --now waydroid-container
```

# 4. Instalar aplicaciones

- Descargar apk y ejecutar:

```
app waydroid instalar <apk>.apk
```