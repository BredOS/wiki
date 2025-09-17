---
title: Radxa Orion O6
description:
published: false
date: 2025-09-17T06:13:49.328Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. Introducción

El Radxa Orion O6 es una placa madre de Minialising ITX alimentada por el Cix P1 (CD8180) SoC, con un núcleo de 12 ARM v9. CPU con 4 corteza grande A720 núm. (~2.8 GHz), 4 A720 medios (~2.4 GHz), y 4 corteza pequeña A520s (~1.8 GHz).  Incluye un GPU G720 de Inmortalis de brazo y un NPU de 30 TOPS para la inferencia de la IA.  Con hasta 64 GB LPDDR5, salidas múltiples de pantalla, red dual 5 GbE y expansión PCIe Gen 4, está dirigido a aplicaciones de edición, multimedia y estaciones de trabajo de desarrolladores.

> Lo apodamos "_Prion_" gracias a las habilidades de escritura de Pandas.
> {.is-info}

# 2. Descargar

Puedes encontrar enlaces de descarga para aarch64 ISO en nuestra [página de Github](https://github.com/BredOS/bredos-iso/releases/latest)!

# 3. Instalación

El Prion soporta la instalación de imágenes ISO genéricas, a diferencia de nuestros otros ordenadores de una sola placa (SBCs) compatibles con imágenes específicas de dispositivos. La instalación se puede realizar usando una memoria USB o incluso una unidad óptica USB.

## 3.1 Instalación ISO genérica

Aquí está disponible una guía para la instalación.

## 3.2 Instalación UEFI

Hemos desarrollado una UEFI personalizada basada en el código fuente de Radxa. Soporta la velocidad real de la CPU a la que se vende la placa, permite controlar la velocidad de enlace de PCIe, y - lo mejor de todo - muestra el logotipo de Bred al inicio. Una guía para actualizar su UEFI está disponible aquí.