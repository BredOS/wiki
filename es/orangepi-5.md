---
title: Serie Naranja Pi 5
description: Esta página contiene enlaces a guías/ajustes útiles para los dispositivos de la Serie OPI 5
published: true
date: 2025-09-21T09:45:58.585Z
tags: opi, opi-5
editor: markdown
dateCreated: 2024-20T15:17:37.567Z
---

# 1. Dispositivos de la Serie Orange Pi 5 compatibles

| Dispositivo        | UEFI | Soportado | Problemas conocidos                                       |
| ------------------ | ---- | --------- | --------------------------------------------------------- |
| Pi Naranja 5       | Sí   | Sí        | SSDs de Sata M.2 puede no funcionar       |
| Pi naranja 5B      | Sí   | Sí        | Usa la imagen OPI5 y requiere DTBO para que funcione wifi |
| Pi Naranja 5 Plus  | Sí   | Sí        |                                                           |
| Naranja Pi 5 Pro   | Nu   | Sí        |                                                           |
| Pi Naranja 5       | Nu   | Sí        |                                                           |
| Pi Naranja 5 Ultra | Nu   | Sí        |                                                           |
| CM5 de Pi Naranja  | Nu   | Sí        |                                                           |

> El Orange Pi 5, 5B y 5 Pro utilizan RK3588S, mientras que los 5 Plus y 5 Max usan RK3588 (que tienen más carriles de PCI y mipi disponibles)
> {.is-info}

### Tabset {.tabset}

#### Pi Naranja 5

> Lo apodamos "_opi5_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: Rockchip RK3588S, Núcleo de 8 cm (Cortex. A76 @ ~2.4GHz + 4×Cortex A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- Almacenamiento: ranura microSD; NVMe M.2 vía PCIe; sin socket eMMC por defecto (solo flash)
- Vídeo / Display: HDMI2.1 hasta 8K@60Hz; puerto USB C DisplayPort; doble salida MIPI D.UPHY; múltiples
- Conectividad: Ethernet Gigabit, WiFi/BT opcional vía M.2 o módulos dependiendo de la versión; otros puertos, etc.
- Poder: 5V/4A
- Tamaño del tablero ~100 × 62 mm.

#### Pi Naranja 5 Plus

> Lo apodamos "_opi5b_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5B" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: Rockchip RK3588S, Núcleo de 8 cm (Cortex. A76 @ ~2.4GHz + 4×Cortex A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- Almacenamiento: 32GB eMMC en muchas variantes; también MicroSD; sin ranura de teclas M.2 para NVMe (o limitado) en algunos modelos?
- Display/video: HDMI2.1 hasta 8K@60Hz; DisplayPort a través de USB C; líneas MIPI etc.
- Conectividad: módulo WiFi6 + BT5.0; Gigabit Ethernet; etc.
- Poder: 5V/4A
- Tamaño del tablero ~100 × 62 mm.

#### Pi Naranja 5

> Lo apodamos "_opi5plus_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5 Plus" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: Rockchip RK3588 (no S), núcleo de 8 (4×Cortex.UA76 @ ~2.4GHz + 4×CortexA55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- Almacenamiento: incluye módulos, NVMe etc.
- Video / Display: altas resoluciones, múltiples HDM/MIPI etc.
- Conectividad: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.

#### CM5 de Pi Naranja

> Lo apodamos "_opi5pro_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5 Pro" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: RK3588S (8nm), Núcleo de 8 grados (4×Cortex A76 @ ~2.4GHz + 4×Cortex.UA55 @ ~1.8GHz)
- RAM: LPDDR5, opciones 4/8/16 GB
- Almacenamiento: MicroSD, socket eMMC o flashear SPI; Tecla M.2 para NVMe/SATA, etc.
- Video: Doble HDMI (HDMI2.1 y HDMI2.0); soporte hasta 8K@60Hz; MIPI DSI etc.
- Conectividad: Gigabit Ethernet; WiFi5 + BT5.0; tarjeta más pequeña (89×56 mm) que la normal 5/5B.
- Poder y otras interfaces también se desplazaron.

#### Naranja Pi 5 Pro

> Lo apodamos "_opi5max_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5 Max" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: Rockchip RK3588 (no S), núcleo de 8 (4×Cortex.UA76 @ ~2.4GHz + 4×CortexA55 @ ~1.8GHz)
- RAM: LPDDR5, opciones 4/8/16 GB
- Almacenamiento: sockets eMMC (32 de 256 GB opcional), microSD, ranura NVMe MA.
- Video: 2× HDMI2.1 hasta 8K@60Hz; MIPI DSI; etc.
- Conectividad: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.
- Tamaño del tablero ~89×57 mm.

#### Pi Naranja 5 Ultra

> Lo apodamos "_opi5ultra_" porque, sinceramente, nadie tiene el tiempo, la paciencia, o incluso el deseo de prueba desenfrenado de decir o escribir constantemente lo ridículamente largo, innecesariamente formal, y ligeramente molesto nombre "Orange Pi 5 Ultra" — especialmente cuando todo el mundo sabe exactamente lo que quiere decir de todos modos.
> {.is-info}

Especificaciones:

- SoC: Rockchip RK3588 (no S), núcleo de 8 (4×Cortex.UA76 @ ~2.4GHz + 4×CortexA55 @ ~1.8GHz)
- RAM: LPDDR5, opciones 4/8/16 GB
- Almacenamiento: sockets eMMC (32 de 256 GB opcional), microSD, ranura NVMe MA.
- Video: 2× HDMI2.1 hasta 8K@60Hz; MIPI DSI; etc.
- Conectividad: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.
- Tamaño del tablero ~89×57 mm.

#### Pi naranja 5B

> Lo apodamos "_opicm5_" porque es más corto.
> {.is-info}

Especificaciones:

- SoC: RK3588S (8nm)
- RAM: LPDDR4/4x, opciones: 2/4/8/16 GB
- Almacenamiento: eMMC a bordo (hasta 256GB), microSD, ampliable a través de M.2 Key.UM etc en la base / carrier boards; soporte para SATA o PCIe dependiendo de la interfaz.
- Video: HDMI2.1 o eDP, MIPI DSI TX, etc; soporte de vídeo 8K; múltiples interfaces de cámara.
- Conectividad: WiFi5 + BT5 (AP6256), puertos USB, etc.
- Físico: factor de forma de módulo; requiere tarjeta base o portador; módulo de tamaño ~40×55 mm.

# 2. Descargar

¡Puedes encontrar enlaces de descarga para imágenes en nuestra [website](https://bredos.org/download.html)!