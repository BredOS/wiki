---
title: Usando DTSC
description: Usando el script de ayuda de compilador de código fuente BredOS Device Tree
published: true
date: 2025-05-07T13:18:58.737Z
tags: null
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# DTSC

`dtsc` es un comando enviado por defecto junto con BredOS junto con el paquete `bredos-tools`.
Para que funcione sin embargo necesitas instalar `dtc`, simplemente ejecuta `yay -S dtc`

El script es un envoltorio a dtsc, realizando preprocesado automático de gcc, enlazando y generando archivos necesarios.
Hace que la generación y la prueba de los árboles de dispositivos sea mucho más sencilla.
Determina y genera automáticamente árboles de dispositivos base o superposiciones en consecuencia.

## NOTA IMPORTANTE

**Instalar un árbol de dispositivo incorrecto en tu consola lo hará inoperable.**
**Ten cuidado, realiza copias de seguridad y asegura un plan de contigencia.**