---
title: Ejecutar aplicaciones Android (waydroid)
description:
published: true
date: 2025-09-26T10:03:46.309Z
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

Necesitas activar y configurar el panthor. Para hacer esto, sigue [esta guía] (/how-to/how-to-setup-panthor).

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

- Luego inicia tu contenedor waydroid-con:

```
inicio de sesión waydroid
```

# 4. Instalar aplicaciones

- Descargar apk y ejecutar:

```
app waydroid instalar <apk>.apk
```

# 4. Instalar aplicaciones

Waydroid por defecto siempre se ejecuta en pantalla completa.

- Si desea que waydroid se integre con su Administrador de Ventanas de entornos de Escritorio, ejecute:

```
prop waydroid establecer persist.waydroid.multi_windows true
```

Luego reinicie la sesión de waydroid.