---
title: Guía de limpieza del espacio en disco
description: Esta guía le guiará a través de varios métodos para recuperar espacio en disco en su sistema BredOS.
published: true
date: 2025-09-16T10:42:55.802Z
tags:
editor: markdown
dateCreated: 2024-20T20:26:57.698Z
---

# 1. Introducción

Con el tiempo, su sistema puede acumular archivos innecesarios que ocupan un espacio valioso. Esta guía le guiará a través de varios métodos para recuperar espacio en disco en su sistema BredOS.

# 2. Limpiar caché de paquetes

Al instalar o actualizar paquetes, `pacman` mantiene en caché copias en `/var/cache/pacman/pkg/` para hacer que la reinstalación sea más rápida. Sin embargo, estos paquetes almacenados en caché pueden acumularse y consumir espacio en disco.

## 2.1 Comprobar tamaño de caché

- Para ver lo grande que es la caché de paquetes, ejecute:

```
du -sh /var/cache/pacman/pkg/
```

## 2.2 Limpieza manual

- Puede eliminar manualmente los paquetes en caché que ya no están instalados con:

```
sudo pacman -Sc
```

## 2.3 Limpieza automática con dolor de Pacc

También puedes usar `paccache` para mantener sólo las 3 versiones más recientes de cada paquete:

- Instalar la herramienta necesaria:

```
   sudo pacman -S pacman-contrib
```

- Configurar un gancho Pacman para limpiar automáticamente después de cada transacción:

```
   sudo nano /usr/share/libalpm/hooks/paccache.hook
```

- Añadir el siguiente contenido al archivo:

```
   [Trigger]
   Operación = Actualizar
   Operación = Instalar
   Operación = Quitar
   Tipo = Paquete
   Objetivo = *

   [Action]
   Descripción = Limpiar caché pacman con paccache…
   Cuando = PostTransaction
   Exec = /usr/bin/paccache -r
```

- Guarda el archivo con **Ctrl + S** y sal con **Ctrl + X**.

# 3. Limpiar archivos antiguos de registro

- Los registros del sistema pueden ocupar una cantidad considerable de espacio a lo largo del tiempo. Puedes comprobar el tamaño de tus registros con:

```bash
journalctl --uso de disco
```

## 3.1 Limpiar registros antiguos

- Para eliminar registros anteriores a 3 días:

```bash
sudo diario --vacuum-time=3d
```

# 4. Usar BleachBit

BleachBit es una poderosa herramienta que le ayuda a limpiar la basura del sistema, a liberar espacio en disco y a proteger su privacidad. Puedes aprender más sobre cómo usar BleachBit [here](https://www.bleachbit.org/).

# 5. Limpiar caché de usuario

- A medida que usas tu sistema, los cachés se acumularán en tu directorio personal. Puede comprobar el tamaño de su carpeta de caché con:

```bash
sudo du -sh ~/.cache/
```

## 5.1 Limpiar el caché

- Para eliminar todos los archivos de caché:

```bash
rm -rf ~/.cache/*
```

---

# 5. Buscar archivos y directorios grandes

A veces, archivos grandes pueden ocupar espacio innecesariamente. Aquí están las herramientas que puede utilizar para identificarlas:

## 6.1 Herramientas de Consola

- **duc** — Un inspector de uso de disco.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\\
  **duc** — Un inspector de uso de disco.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- **gdu** — Analizador de uso de disco con interfaz de consola.\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`

- **ncdu** — ncurses el analizador de uso de disco.\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  **duc** — Un inspector de uso de disco.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  **duc** — Un inspector de uso de disco.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

## 6.2 Herramientas Gráficas

- **Filelight** — Mapa de uso de disco interactivo con anillos concentrados.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\\
  **Filelight** — Mapa de uso de disco interactivo con anillos concentrados.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`

- **Analizador de uso de discos GNOME (baobab)** — Analizador de uso de discos para GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\\
  **Analizador de uso de discos GNOME (baobab)** — Analizador de uso de discos para GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **Analizador de uso de discos GNOME (baobab)** — Analizador de uso de discos para GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`

- **Filelight** — Mapa de uso de disco interactivo con anillos concentrados.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  **Filelight** — Mapa de uso de disco interactivo con anillos concentrados.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  **qdirstat** — Herramienta de estadísticas de directorio basadas en Qt.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  **qdirstat** — Herramienta de estadísticas de directorio basadas en Qt.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`

---

> ¡Libera espacio y mantén tu sistema BredOS funcionando sin problemas!
> {.is-success}

