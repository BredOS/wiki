---
title: Configuración de BredOS
description:
published: false
date: 2025-09-21T09:27:32.905Z
tags:
editor: markdown
dateCreated: 2025-09-21T09:27:04.136Z
---

# 1. Introducción

- La herramienta `bredos-config` ha sido desarrollada para simplificar los cambios, mantenimiento y gestión del sistema para usted.

![main.png](/bredos-config/main.png)

> La herramienta `bredos-config` está instalada por defecto.
> {.is-info}

- Si lo eliminó y/o desea reinstalarlo, ejecute:

```
sudo pacman -S bredos-config
```

# 2. Características

## 2.1 Gestor de Árbol de Dispositivos

- Esta opción le ayuda a administrar los árboles de dispositivos y superposiciones del árbol de dispositivos, los cuales se usan para alterar cómo el núcleo interactúa con su dispositivo. Un ejemplo simple sería utilizarlos para desactivar el LED en un Narange Pi 5 Plus, pero hay mucho más que explorar. Sigue [este artículo](/how-to/how-to-enable-dtbos) para aprender más sobre él.

![dtb-manager.png](/bredos-config/dtb-manager.png)

## 2.2 Actualizar el sistema

> ¡Esta opción está actualmente en construcción!
> {.is-warning}

## 2.3 Mantenimiento del Sistema

- En esta sección, encontrará algunas tareas útiles para mantener su sistema limpio y funcionando sin problemas como Realizar tareas de mantenimiento del sistema de archivos o comprobar la integridad del sistema.

![upkeep.png](/bredos-config/upkeep.png)

## 2.4 Ajustes del sistema

- Aquí puede encontrar algunos ajustes útiles en su sistema:

![tweaks.png](/bredos-config/tweaks.png)

## 2.5 Migraciones

> ¿Por qué no se ha fusionado esto en ajustes del sistema?
> {.is-danger}

## 2.6 Paquetes

- Aquí encontrarás varios ganchos que te ayudarán a instalar cosas geniales, como vapor o docker, correctamente:

![packages.png](/bredos-config/packages.png)