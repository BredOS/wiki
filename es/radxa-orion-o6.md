---
title: Radxa Orion O6
description:
published: false
date: 2025-09-17T09:09:38.481Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. Introducción

Orion O6 es una placa ARM64 con formato ITX con grandes especificaciones:

- SoC: CIX CD8180
- CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1.8GHz
- GPU: Inmortales G720 MC10
- NPU: 30 MES
- Red: Ethernet 2x 5Gbit (PCIe 4.0 1x carril cada uno)

Puertos PCIe:

- Clave M.2 M (carriles PCIe 4.0 4x)
- Clave M.2 E (carriles PCIe 4.0 2x)
- Ranura PCIe x16 de tamaño completo (carriles PCIe 4.0 8x)

> Lo apodamos "_Prion_" gracias a las habilidades de escritura de Pandas.
> {.is-info}

# 2. Descargar

Puedes encontrar enlaces de descarga para aarch64 ISO en nuestra [página de Github](https://github.com/BredOS/bredos-iso/releases/latest)!

Tenemos dos versiones disponibles: una basada en el núcleo 6.6 de Radxa, y la otra en la línea principal.
La versión basada en el núcleo 6.6 tiene el nombre de "ORION" adjunto y tiene soporte para el conjunto completo de características de ese tablero.
El núcleo principal tiene controladores faltantes. Un resumen de lo que trabaja en la línea principal y lo que no se puede encontrar en la sección `4. Soporte de línea principal`.

# 3. Instalación

El Prion soporta la instalación de imágenes ISO genéricas, a diferencia de nuestros otros ordenadores de una sola placa (SBCs) compatibles con imágenes específicas de dispositivos. La instalación se puede realizar usando una memoria USB o incluso una unidad óptica USB.

## 3.1 Instalación ISO genérica

Aquí está disponible una guía para la instalación genérica .is.

## 3.2 Instalación UEFI

Hemos desarrollado una UEFI personalizada basada en el código fuente de Radxa. Soporta la velocidad real de la CPU a la que se vende la placa, permite controlar la velocidad de enlace de PCIe, y - lo mejor de todo - muestra el logotipo de Bred al inicio. Una lista completa de características y una guía para actualizar tu UEFI está disponible [here](/en/radxa-orion-o6/prion-uefi-installation).

# 4. Soporte en línea principal

| `linux`                     | Estado  | Notas                                                                                                                                                                                                                        |
| --------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Línea principal             | Obras   |                                                                                                                                                                                                                              |
| CPU                         | Obras   |                                                                                                                                                                                                                              |
| RAM                         | Obras   |                                                                                                                                                                                                                              |
| GPU                         | Rota    | Sin conductor                                                                                                                                                                                                                |
| NPU                         | Rota    | Sin conductor                                                                                                                                                                                                                |
| Codificar HW                | Rota    | Sin conductor                                                                                                                                                                                                                |
| Decodificar HW              | Rota    | Sin conductor                                                                                                                                                                                                                |
| HDMI                        | Parcial | EFI FB funciona parcialmente (1080P@60Hz en la mayoría de los monitores)                                                                                                                     |
| DP                          | Parcial | Igual que arriba                                                                                                                                                                                                             |
| DP USB-C                    | Parcial | Igual que arriba                                                                                                                                                                                                             |
| Almacenamiento              | Obras   | SSDs M.2 como se esperaba                                                                                                                                                                                    |
| Ethernet                    | Obras   |                                                                                                                                                                                                                              |
| USB frontal                 | Obras   | Al azar muere, necesita bifurcación BredOS personalizada de Radxa bios                                                                                                                                                       |
| Ejecutar USB                | Obras   | Al azar muere, necesita bifurcación BredOS personalizada de Radxa bios                                                                                                                                                       |
| Audio frontal               | Rota    | Sin conductor                                                                                                                                                                                                                |
| Audio de Rear               | Rota    | Sin conductor                                                                                                                                                                                                                |
| RTC                         | Obras   | Sin conductor                                                                                                                                                                                                                |
| UART                        | Obras   | `ttyS2` al arrancar                                                                                                                                                                                                          |
| PCI                         | Parcial | Funciona bien en la mayoría de los dispositivos pero algunos GPU no funcionan como se esperaba. <br> congela todo el sistema a veces. Considere el uso de nuestra biografía. |
| Llave M.2 E | Obras   |                                                                                                                                                                                                                              |
| Llave M.2 M | Obras   |                                                                                                                                                                                                                              |
| Control de ventilador       | Obras   | Control de ventilador automático, no hay forma de controlar desde el sistema operativo                                                                                                                                       |

# 5. PCI

Algunos testers han encontrado que el sistema se vuelve inestable cuando un dispositivo que opera en PCIe Gen. 4 velocidades está conectado. Si su tablero es inestable debido a esto, considere actualizar a nuestro firmware UEFI y ajustar la velocidad del enlace al General 3.