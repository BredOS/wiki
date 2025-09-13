---
title: 🎮 Cómo instalar STEAM en BredOS
description: Una guía simple para instalar Steam en BredOS, con instrucciones paso a paso para configuraciones Panthor-enabled y no Panthor.
published: true
date: 2025-09-13T09:15:38.539Z
tags:
editor: markdown
dateCreated: 2024-08T09:55:58.661Z
---

# 🎮 Cómo instalar Steam en BredOS

Bienvenido a la guía sobre cómo instalar **Steam** en BredOS! Siga estos sencillos pasos para que Steam funcione en su sistema.

## 🛠️ 1. Prerrequisitos

> Esto puede no funcionar en todos los dispositivos (principalmente dispositivos no RK35888).
> {.is-info}

- Necesitas tener **BredOS** instalado y funcionando.
- Opcionalmente, puedes tener [**Panthor** activado](/how-to/how-to-setup-panthor), pero no es necesario.

## 📥 2. Pasos de instalación

### 🤖 2.1 Automáticamente

La herramienta `bredos-config` ofrece una forma simple de instalar Steam y las librerías de vapor apropiadas. Iniciar la herramienta con

```
sudo bredos-config
```

y navega a `Packages` -> `Install Steam`. Entonces se instalará Steam. Fácil, ¿verdad?

### 🦶 2.2 Manualmente

#### 🔄 2.2.1 En caso de usar una imagen BredOS antigua:

Puede que tengas que añadir el repositorio **BredOS Multíb** para instalar Steam y las capas de traducción necesarias. Para hacer esto, siga estos pasos:

- Instala el paquete `bredos-multilib`

```
   sudo pacman -S bredos-multilib
```

- Actualice la base de datos de paquetes ejecutando:

```
   sudo pacman -Sy
```

---

#### 🖥️ 2.2.2 Instalación de Steam:

- Ejecutar el siguiente comando para instalar Steam:

```
   sudo pacman -S steam
```

- Después de ejecutar el comando, verá un mensaje que le pedirá que seleccione una opción. Elija la opción apropiada basándose en su configuración:

  - Primero, selecciona `lib32-vulkan-swrast`

![steam\\_libs\\_selection.png](/steam_libs_selection.png)

- Si tienes habilitado **Panthor**, selecciona `steam-libs-any`.

- Si **Panthor** no está habilitado (usando Panfork en su lugar), selecciona `steam-libs-rk3588`.

- Espere a que se complete la instalación y ya está todo listo! 🎉

## 🔄 3. Desinstalando Steam

Si necesitas desinstalar Steam y restablecer la configuración para elegir una opción diferente:

```
sudo pacman -Rnscu Steam-libs-any #o steam-libs-rk3588 dependiendo de su selección
```

## 🚀 4. Lanzar Steam

Una vez finalizada la instalación, puede iniciar Steam buscando en el menú de su aplicación o ejecutando:

```
vapor
```

> **¡Juego Feliz! 🎮✨**
> {.is-success}

