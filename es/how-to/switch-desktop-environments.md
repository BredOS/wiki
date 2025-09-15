---
title: Cambiar entornos de escritorio en BredOS
description: Aprende cómo instalar y cambiar al entorno de escritorio GNOME en BredOS
published: true
date: 2025-09-15T10:00:53.184Z
tags: personalización
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 1. Escritorio GNOME en BredOS

## 1.1 Install Gnome

El entorno de escritorio GNOME se puede instalar con el paquete `gnome`.\
Para instalarlo, ejecutar:

- Para instalarlo, ejecutar:

```
pacman -S gnome
```

Se pueden instalar paquetes gnome adicionales con `gnome-circle` que contiene varias aplicaciones extra que extienden el ecosistema GNOME y `gnome-extra` que contienen herramientas de desarrollo así como otras aplicaciones y juegos que encajen bien en GNOME.

---

## 1.2 Cambiar a GDM

Para una operación adecuada, necesitas cambiar a **GDM** después de la instalación.\
Ejecutar los siguientes comandos:\
Ejecutar los siguientes comandos:

- Ejecutar los siguientes comandos:

```
sudo systemctl deshabilita lightdm
sudo systemctl habilitar gdm
```

> 📝 **Nota:** Sólo se admite GNOME en Wayland.
> {.is-warning}

---

## Arreglo de rotación de pantalla 1.3

**Si** tu pantalla gira incorrectamente, puedes instalar y configurar la extensión **Rotación de pantalla**.

### 1.3.1 Instalar el gestor de extensiones

- Ejecutar:

```
sudo pacman -S extension-manager
```

Una vez instalado, abre la aplicación.

### 1.3.2 Instalar Pantalla Rotar

Dentro de la aplicación:

- Pulsa `Buscar` > `Buscar`
- Tipo **Rotación de pantalla**
- Instala `Screen Rotate` por **shyzus**.

### 1.3.3 Configurar rotación de pantalla

- Ve a la pestaña `Installed` en el Administrador de extensiones.
- Toca el icono ⚙️ para abrir la configuración de la extensión.
- Incremente el valor **Establecer desplazamiento de orientación** a `1`.

# 2. Escritorio de plasma en BredOS

## 2.1 Install KDE Plasma

El entorno de escritorio de Plasma se puede instalar con el paquete `plasma-desktop`.\
Para instalarlo, ejecutar:

- Para instalarlo, ejecutar:

```
pacman -S plasma-desktop
```

Esto debería resultar en una instalación mínima del escritorio de plasma. Para instalar una experiencia de KDE más completa, elija el paquete `plasma` (que le permite elegir qué paquetes de plasma desea instalar) o `plasma-meta` para obtener la cosa completa. Haga clic en [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) para entender la diferencia entre un grupo y un metpaquete.

> Evite el uso de SDDM ya que este software es abandonado! LightDM funciona bien con plasma.
> {.is-warning}
