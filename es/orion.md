---
title: Serie Orion Radxa
description:
published: false
date: 2025-09-17T00:28:55.869Z
tags:
editor: markdown
dateCreated: 2025-09-17T00:08:50.283Z
---

# Introducción

SoC: CIX CD8180
CPU: 4x A72 @ 2.6GHz + 4x A72 @ 2.4GHz + 4x A52 @ 1. GHz
GPU: Inmortals G720 MC10
NPU: 30 TOonancia
Red: 2x Ethernet 5Gbit (PCIe 4.0 1x carril cada una)
PCIe:

- Clave M.2 M (carriles PCIe 4.0 4x)
- Clave M.2 E (carriles PCIe 4.0 2x)
- Ranura PCIe x16 de tamaño completo (carriles PCIe 4.0 8x)

# Soporte en línea principal

| `linux`                     | Estado  | Notas                                                                                                                                                |
| --------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Línea principal             | Obras   |                                                                                                                                                      |
| CPU                         | Obras   |                                                                                                                                                      |
| RAM                         | Obras   |                                                                                                                                                      |
| GPU                         | Rota    | Sin conductor                                                                                                                                        |
| NPU                         | Rota    | Sin conductor                                                                                                                                        |
| Codificar HW                | Rota    | Sin conductor                                                                                                                                        |
| Decodificar HW              | Rota    | Sin conductor                                                                                                                                        |
| HDMI                        | Parcial | EFI FB funciona parcialmente (1080P@60Hz en la mayoría de los monitores)                                             |
| DP                          | Parcial | Igual que arriba                                                                                                                                     |
| DP USB-C                    | Parcial | Igual que arriba                                                                                                                                     |
| Almacenamiento              | Obras   | SSDs M.2 como se esperaba                                                                                                            |
| Ethernet                    | Obras   |                                                                                                                                                      |
| USB frontal                 | Obras   | Al azar muere, necesita bifurcación BredOS personalizada de Radxa bios                                                                               |
| Ejecutar USB                | Obras   | Al azar muere, necesita bifurcación BredOS personalizada de Radxa bios                                                                               |
| Audio frontal               | Rota    | Sin conductor                                                                                                                                        |
| Audio de Rear               | Rota    | Sin conductor                                                                                                                                        |
| RTC                         | Obras   | Sin conductor                                                                                                                                        |
| UART                        | Obras   | `ttyS2` al arrancar                                                                                                                                  |
| PCI                         | Parcial | Funciona bien en la mayoría de los dispositivos pero algunos GPU no funcionan como se esperaba. <br> congela todo el sistema a veces |
| Llave M.2 E | Obras   |                                                                                                                                                      |
| Llave M.2 M | Obras   |                                                                                                                                                      |
| Control de ventilador       | Obras   | Control de ventilador automático, no hay forma de controlar desde el sistema operativo                                                               |