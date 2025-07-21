---
title: Cambiar entornos de escritorio para usar GNOME en BredOS
description: Aprende cómo instalar y cambiar al entorno de escritorio GNOME en BredOS
published: true
date: 2025-02-23T15:13:50.035Z
tags: personalización
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 🎨 Escritorio GNOME en BredOS

El entorno de escritorio GNOME se puede instalar con el paquete AUR `gnome-meta`.\
Para instalarlo, ejecutar:\
Para instalarlo, ejecutar:\
Para instalarlo, ejecutar:

```
yay -S gnome-meta
```

---

## 🔄 Cambiar a GDM

Para una operación adecuada, necesitas cambiar a **GDM** después de la instalación.\
Ejecutar los siguientes comandos:\
Ejecutar los siguientes comandos:\
Ejecutar los siguientes comandos:

```
sudo systemctl deshabilita lightdm
sudo systemctl habilitar gdm
```

📝 **Nota:** Sólo se admite GNOME en Wayland.

---

## 🔄 🖥️ Reparar rotación de pantalla

**Si** tu pantalla gira incorrectamente, puedes instalar y configurar la extensión **Rotación de pantalla**.

### 1️⃣ Instalar el gestor de extensiones

Ejecutar:

```
sudo pacman -S extension-manager
```

Una vez instalado, abre la aplicación.

### 2️⃣ Instalar la rotación de pantalla

Dentro de la aplicación:

- Pulsa `Buscar` > `Buscar`
- Tipo **Rotación de pantalla**
- Instala `Screen Rotate` por **shyzus**.

### 3️⃣ Configurar rotación de pantalla

- Ve a la pestaña `Installed` en el Administrador de extensiones.
- Toca el icono ⚙️ para abrir la configuración de la extensión.
- Incremente el valor **Establecer desplazamiento de orientación** a `1`.

---

✅ ¡Hecho! GNOME ahora está configurado correctamente en BredOS. 🚀
