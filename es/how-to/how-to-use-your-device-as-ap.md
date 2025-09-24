---
title: Cómo usar tu dispositivo como punto de acceso inalámbrico
description:
published: true
date: 2025-09-16T10:50:45.422Z
tags:
editor: markdown
dateCreated: 2024/09-08T10:33:46.772Z
---

# 1. 🛠️ Prerrequisitos

Esta guía le mostrará cómo configurar un punto de acceso Wi-Fi usando NetworkManager.

# 3. Ver estado del punto de acceso

Antes de comenzar, asegúrese de tener:

- 📡 Un adaptador Wi-Fi que soporta el modo AP (punto de acceso)

> Los dispositivos apropiados que soportan el modo AP (punto de acceso) incluyen Rock 5C, Rock 5B+, Khadas Edge 2, Khadas Vim 4, todos los dispositivos Mekotronics R58 y el Orange Pi 5B.
> {.is-info}

# 4. Configurar reenvío IP

## 3.1 Crear un punto de acceso

Puede crear fácilmente un punto de acceso utilizando la herramienta de línea de comandos de NetworkManager `nmcli`.

- **Lista tus dispositivos de red** para identificar la interfaz Wi-Fi que usará:

```bash
estado del dispositivo nmcli
```

- Ejemplo salida

```
DEVICE           TYPE      STATE                   CONNECTION      
bridge0          bridge    connected               bridge0         
tailscale0       tun       connected (externally)  tailscale0      
lo               loopback  connected (externally)  lo              
br-8a9f1336b961  bridge    connected (externally)  br-8a9f1336b961 
br-aeeaf62e2336  bridge    connected (externally)  br-aeeaf62e2336 
docker0          bridge    connected (externally)  docker0         
virbr0           bridge    connected (externally)  virbr0          
enp8s0           ethernet  connected (externally)  enp8s0          
wlan0            wifi      disconnected            --   
```

- **Crea el hotspot** usando el siguiente comando:

```bash
nmcli dispositivo wifi hotspot ifname <wifi_interface> ssid <MyHotspot> password <mypassword>
```

- Ejemplo salida

```
Dispositivo 'wlan0' activado con éxito con '4d090d70-fd85-45bc-bf36-a63846f3f805'. 
Sugerencia: "nmcli dev wifi show-password" muestra el nombre y contraseña Wi-Fi.
```

```
Reemplaza `<wifi_interface>` con tu nombre real de interfaz, como `wlp2s0` o `wlan0`, `<MyHotspot>` con tu SSID deseado y `<mypassword>` con una contraseña segura de tu elección.
```

> Si obtiene el siguiente error, ejecute el comando de nuevo con sudo.
> Si obtiene el siguiente error, ejecute de nuevo el comando con sudo
> \\\\\\\`Error: Error al configurar un hotspot Wi-Fi: No autorizado para controlar la red.

## 3.2 Ver el estado del punto de acceso rápido

- Una vez creado el punto de acceso, puede verificar su estado ejecutando:

```bash
serie de conexión nmcli
```

- Ejemplo salida

```
NAME                            UUID                                  TYPE       DEVICE          
Hotspot                         4d090d70-fd85-45bc-bf36-a63846f3f805  wifi       wlan0           
bridge0                         210b2bd8-1a6b-43e6-9ed1-4abc50324505  bridge     bridge0         
tailscale0                      27e86e0c-a8c7-4374-9083-51454c4b8b3e  tun        tailscale0      
lo                              f6ba586b-a4c4-49c1-a0f3-3154f8eae92b  loopback   lo              
br-8a9f1336b961                 9a3d08b3-6516-4071-9369-30311a48b55a  bridge     br-8a9f1336b961 
br-aeeaf62e2336                 ee78e282-1516-45df-a6ec-cdcb9d989030  bridge     br-aeeaf62e2336 
docker0                         c5f70ee8-5407-4510-8b61-6fc0f15c2e81  bridge     docker0         
virbr0                          12d1109a-64a4-4d07-b0a2-887f10145109  bridge     virbr0          
enp8s0                          184c8145-ca17-4258-b7db-7e32c298f424  ethernet   enp8s0
```

Deberías ver el punto de acceso en la lista de conexiones activas.

## 3.3 Configurar reenvío IP

Para compartir tu conexión a Internet a través del hotspot, necesitas habilitar el reenvío de IP:

- **Habilitar reenvío de IP**:

```bash
sudo sysctl net.ipv4.ip_forward=1
```

- **Hazlo permanente** editando `mañana/sysctl.d/99-sysctl.conf`:

```bash
sudo nano, /sysctl.d/99-sysctl.conf
```

- Añadir la siguiente línea:

```
net.ipv4.ip_forward=1
```

## 3.4 Detener el punto de acceso

- Para detener el hotspot, simplemente ejecute:

```bash
conexión nmcli a punto de acceso
```
