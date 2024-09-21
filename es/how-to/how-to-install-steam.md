---
title: 🎮 Cómo instalar STEAM en BredOS
description: Una guía simple para instalar Steam en BredOS, con instrucciones paso a paso para configuraciones Panthor-enabled y no Panthor.
published: true
date: 2024/09-08T10:37:48.498Z
tags: null
editor: markdown
dateCreated: 2024-08T09:55:58.661Z
---

# 🎮 Cómo instalar Steam en BredOS

Bienvenido a la guía sobre cómo instalar **Steam** en BredOS! Siga estos sencillos pasos para que Steam funcione en su sistema.

## 🛠️ Prerrequisitos

> Nota: Steam parece funcionar sólo en escritorios X11. Además, es posible que no funcione en todos los dispositivos (principalmente en dispositivos no RK35888).
> {.is-info}

- Necesitas tener **BredOS** instalado y funcionando.
- Opcionalmente, puedes tener [**Panthor** activado](/es/how-to/how-to-setup-panthor), pero no es necesario.

## 📥 Pasos de instalación

### 🔄 En caso de usar una imagen BredOS antigua:

Puede que tengas que añadir el repositorio **BredOS Multíb** para instalar Steam y las capas de traducción necesarias. Para hacer esto, siga estos pasos:

1. Instala el paquete `bredos-multilib`

```
   sudo pacman -S bredos-multilib
```

2. Actualice la base de datos de paquetes ejecutando:

```
   sudo pacman -Sy
```

---

### 🖥️ Instalación de Steam:

1. Abra su terminal 🖥️.
2. Ejecutar el siguiente comando para instalar Steam:

```
   sudo pacman -S steam
```

3. Después de ejecutar el comando, verá un mensaje que le pedirá que seleccione una opción. Elija la opción apropiada basándose en su configuración:

   - Primero, selecciona `lib32-vulkan-swrast`

![steam\\\_libs\\\_selection.png](/steam_libs_selection.png)

- Si tienes habilitado **Panthor**, selecciona `steam-libs-any`.
- Si **Panthor** no está habilitado (usando Panfork en su lugar), selecciona `steam-libs-rk3588`.

4. Espere a que se complete la instalación y ya está todo listo! 🎉

## 🔄 Desinstalar Steam

Si necesitas desinstalar Steam y restablecer la configuración para elegir una opción diferente:

```
sudo pacman -Rnscu Steam-libs-any #o steam-libs-rk3588 dependiendo de su selección
```

## 🚀 Lanzamiento Steam

Una vez finalizada la instalación, puede iniciar Steam buscando en el menú de su aplicación o ejecutando:

```
vapor
```

**¡Juego Feliz! 🎮✨**
