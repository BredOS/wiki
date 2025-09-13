---
title: Cómo usar tu dispositivo como punto de acceso inalámbrico
description:
published: true
date: 2025-09-13T10:44:39.156Z
tags:
editor: markdown
dateCreated: 2024/09-08T10:33:46.772Z
---

# 📶 Cómo configurar un punto de acceso usando NetworkManager

Esta guía le mostrará cómo configurar un punto de acceso Wi-Fi usando NetworkManager.

## 1. 🛠️ Prerrequisitos

Antes de comenzar, asegúrese de tener:

- 📡 Un adaptador Wi-Fi que soporta el modo AP (punto de acceso)

> Los dispositivos apropiados que soportan el modo AP (punto de acceso) incluyen Rock 5C, Rock 5B+, Khadas Edge 2, Khadas Vim 4, todos los dispositivos Mekotronics R58 y el Orange Pi 5B.
> {.is-info}

## 2. Crear un punto de acceso

Puede crear fácilmente un punto de acceso utilizando la herramienta de línea de comandos de NetworkManager `nmcli`.

1. **Lista tus dispositivos de red** para identificar la interfaz Wi-Fi que usará:

   ```bash
   estado del dispositivo nmcli
   ```

2. **Crea el hotspot** usando el siguiente comando:

   ```bash
   nmcli dispositivo wifi hotspot ifname <wifi_interface> ssid <MyHotspot> password <mypassword>
   ```

   Reemplaza `<wifi_interface>` con tu nombre real de interfaz, como `wlp2s0` o `wlan0`, `<MyHotspot>` con tu SSID deseado y `<mypassword>` con una contraseña segura de tu elección.

> Si obtiene el siguiente error, ejecute de nuevo el comando con sudo
> \\\\\`Error: Error al configurar un hotspot Wi-Fi: No autorizado para controlar la red.

## 3. Ver estado del punto de acceso

Una vez creado el punto de acceso, puede verificar su estado ejecutando:

```bash
serie de conexión nmcli
```

Deberías ver el punto de acceso en la lista de conexiones activas.

## 4. Configurar reenvío IP

Para compartir tu conexión a Internet a través del hotspot, necesitas habilitar el reenvío de IP:

1. **Habilitar reenvío de IP**:

   ```bash
   sudo sysctl net.ipv4.ip_forward=1
   ```

2. **Hazlo permanente** editando `mañana/sysctl.d/99-sysctl.conf`:

   ```bash
   sudo nano, /sysctl.d/99-sysctl.conf
   ```

   Añadir la siguiente línea:

   ```
   net.ipv4.ip_forward=1
   ```

## 5) 🛑 Detener el punto de acceso

Para detener el hotspot, simplemente ejecute:

```bash
conexión nmcli a punto de acceso
```
