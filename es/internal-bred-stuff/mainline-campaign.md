---
title: Campaña principal
description:
published: false
date: 2025-09-22T18:31:53.209Z
tags:
editor: markdown
dateCreated: 2025-09-22T17:56:04.573Z
---

## Campaña de hito: Soporte principal RK3588 en BredOS

Ahora mismo, las imágenes BredOS para dispositivos RK3588 dependen del crusty Rockchip BSP kernel — un abrazo, código codificado con ductos que es difícil de mantener, inseguro y siempre señala detrás de Linux.

Queremos cambiar esto.

Manteniendo soporte RK3588, BredOS traerá:

- Mantenimiento prolongado (no más hacks de BSP)

- Correcciones de seguridad del núcleo arriba

- Mejor rendimiento y estabilidad

- Soporte en todos los dispositivos RK3588 (SBCs, tableros dev y mini-PCs)

- Una base sólida para el uso de escritorio y servidor ARM64

Se trata de hacer que BredOS — y el ecosistema Linux más amplio — sea mejor para todos que usen hardware RK3588.

## ¿Por qué lo hacemos?

Una pregunta justa que a menudo oímos es: _"¿Acaso no se mantiene el RK35888?"_\
La verdad es: **solo una parte de ella es**.

Mientras que gran parte del trabajo de bajo nivel (como el soporte básico del núcleo) ha llegado a la parte superior, **los elementos esenciales del día a día todavía están rotos o perdidos**:

- Muchos controladores Wi-Fi no funcionan
- Las optimizaciones específicas del dispositivo no están cubiertas por parches genéricos de línea principal

En BredOS, queremos que los dispositivos RK3588 sean **prácticos y pulidos para usuarios reales**. Eso significa:

- Wi-Fi fiable y redes
- Perfiles optimizados de ventiladores (silenciosos cuando está inactivo, enfriando bajo carga)
- Soporte estable GPU y multimedia
- Instalador adecuado e imágenes listas para flashear

Esta campaña no consiste únicamente en “hacer que arranque”. Se trata de hacer que los dispositivos RK3588 sean **realmente utilizables**.

## Beneficios de línea principal

Gracias a nuestros primeros experimentos en la línea principal, ya hemos visto algunas ventajas emocionantes:

- **2× rendimiento de Vulkan** sobre construcciones de BSP y más bienes de GPU
- **Implementación adecuada de la VPU** que no requiere la plataforma personalizada de procesamiento de medios de Rockchip (MPP)
- Capacidad para ejecutar **Chromium o cualquier aplicación acelerada de video** fuera de la caja
- No hay más hacks o recompilaciones personalizadas para cargas de trabajo de vídeo comunes

La línea principal desbloquea estas **mejoras reales y tangibles** tanto para desarrolladores como para usuarios finales, haciendo que los dispositivos RK3588 sean mucho más capaces en el uso diario.

## Cómo puedes ayudar

- **Donación**: Cada contribución nos acerca más a una experiencia de RK3588. Puedes contribuir [here](https://ko-fi.com/Z8Z3I4J0P) o PM @rippanda12
- **Compartir**: Difunde la palabra en comunidades RK3588, foros de SBC y redes sociales.
- **Patrocinador**: Las empresas dependiendo del hardware RK3588 pueden respaldar este hito en niveles más altos (acreditaremos a los patrocinadores en nuestro repositorio y sitio web).

## Lo que intentaremos hacer

1. **Upstreaming y Kernel Work**
   - Reiniciar parches en el núcleo principal

2. **Soporte para Arranque e Instalación**
   - Soporte para flujo de arranque estándar ARM64 (UEFI donde sea posible)
   - Construye imágenes BredOS apropiadas para tarjetas RK3588

3. **Testing & CI**
   - Compilaciones de pruebas automatizadas para tableros populares (por ejemplo, Orange Pi 5, Rock 5B)
   - Integración continua con actualizaciones de la línea principal

4. **Experiencia de usuario**
   - Asegúrate de que el GPU, la red, el almacenamiento y la E/S sean estables
   - Proporcionar imágenes preconstruidas y listas para flashear para usuarios finales

## Donde va el dinero

- Tiempo del desarrollador (núcleo, cargador de arranque, integración de espacio de usuario)
- Infraestructura de CI para construcciones y pruebas en curso

**[Soporte al Hito Principal RK3588 ahora](https://ko-fi.com/Z8Z3I4J0P)**
