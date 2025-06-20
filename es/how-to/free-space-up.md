---
title: 🧹💾 Guía de limpieza de espacio en disco
description: Esta guía le guiará a través de varios métodos para recuperar espacio en disco en su sistema BredOS. 🖥️✨
published: true
date: 2024-09-21T09:03:53.416Z
tags:
editor: markdown
dateCreated: 2024-20T20:26:57.698Z
---

# Guía de limpieza del espacio en disco BredOS 🧹💾

Con el tiempo, su sistema puede acumular archivos innecesarios que ocupan un espacio valioso. Esta guía le guiará a través de varios métodos para recuperar espacio en disco en su sistema BredOS. 🖥️✨

---

## 📚 Índice de contenidos

- Limpiar Caché de Paquetes 📦
- Limpiar archivos antiguos de registro 📝
- Usar BleachBit 🧽
- Limpiar Caché de Usuario 🏠
- Buscar archivos grandes y directorios 📂

---

## Limpiar Caché de Paquetes 📦

Al instalar o actualizar paquetes, **Pacman** mantiene copias en caché en `/var/cache/pacman/pkg/` para hacer que la reinstalación sea más rápida. Sin embargo, estos paquetes almacenados en caché pueden acumularse y consumir espacio en disco.

### Comprobar tamaño de caché 📏

Para ver lo grande que es la caché de paquetes, ejecute:

```bash
du -sh /var/cache/pacman/pkg/
```

### Limpieza manual 🗑️

Puede eliminar manualmente los paquetes en caché que ya no están instalados con:

```bash
sudo pacman -Sc
```

### Limpieza automática con Paccache 🔄

También puedes usar **paccache** para mantener sólo las 3 versiones más recientes de cada paquete:

1. Instalar la herramienta necesaria:
  ```bash
  sudo pacman -S pacman-contrib
  ```
2. Configurar un gancho Pacman para limpiar automáticamente después de cada transacción:
  ```bash
  sudo nano /usr/share/libalpm/hooks/paccache.hook
  ```
  Añadir el siguiente contenido al archivo:
  ```bash
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
  Guarda el archivo con **Ctrl + S** y sal con **Ctrl + X**.

---

## Limpiar archivos antiguos de registro 📝

Los registros del sistema pueden ocupar una cantidad considerable de espacio a lo largo del tiempo. Puedes comprobar el tamaño de tus registros con:

```bash
journalctl --uso de disco
```

### Limpiar Registros Antiguos :jabón:

Para eliminar registros anteriores a 3 días:

```bash
sudo diario --vacuum-time=3d
```

---

## Usar BleachBit 🧽

**BleachBit** es una poderosa herramienta que te ayuda a limpiar la basura del sistema, a liberar espacio en disco y a proteger tu privacidad. Puedes aprender más sobre cómo usar BleachBit [here](https://www.bleachbit.org/).

---

## Limpiar Caché de Usuario 🏠

A medida que usas tu sistema, los cachés se acumularán en tu directorio personal. Puede comprobar el tamaño de su carpeta de caché con:

```bash
sudo du -sh ~/.cache/
```

### Limpiar el caché 🧹

Para eliminar todos los archivos de caché:

```bash
rm -rf ~/.cache/*
```

---

## Buscar archivos grandes y directorios 📂

A veces, archivos grandes pueden ocupar espacio innecesariamente. Aquí están las herramientas que puede utilizar para identificarlas:

### Herramientas de consola ⌨️

- **duc** — Un inspector de uso de disco.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- **gdu** — Analizador de uso de disco con interfaz de consola.\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`

- **ncdu** — ncurses el analizador de uso de disco.\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`

### Herramientas gráficas :framed_imagen:

- **Filelight** — Mapa de uso de disco interactivo con anillos concentrados.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`

- **Analizador de uso de discos GNOME (baobab)** — Analizador de uso de discos para GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`

- **qdirstat** — Herramienta de estadísticas de directorio basadas en Qt.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`

---

¡Libera espacio y mantén tu sistema BredOS funcionando sin problemas! 💪✨
