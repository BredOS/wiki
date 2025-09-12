---
title: Arreglo de firmware de Sata
description:
published: false
date: 2025-09-12T09:18:06.486Z
tags:
editor: markdown
dateCreated: 2025-09-12T09:18:06.486Z
---

# Arreglo de firmware SATA

### 1. Prerrequisitos

- Un flasheador basado en CH341
- Un soldado o un clip SPI
- El nuevo archivo de firmware (descargarlo desde [here])
- Otro dispositivo con Linux instalado (Windows debería funcionar también, pero no está cubierto aquí)

Un paquete muy práctico que incluye el flasher, el clip y otros accesorios útiles puede ser pedido aquí:
https://www.aliexpress.com/item/32263275388.html

### 2. Conectar a SPI

> ⚡ _Antes de conectar cualquier cosa a la potencia, ¡comprueba que todos los conectores estén correctamente orientados!_ ⚡
> {.is-warning}

La forma más sencilla de conectarse al chip SPI es usando el clip. Puede ser un poco complicado conseguir una conexión firme, pero no requiere ninguna habilidad de soldadura o herramientas. Además, es muy poco probable que el uso del clip cause algún daño en el foro.

Por otro lado, si tienes experiencia de soldadura, no es una tarea difícil desenvejecer y resolver los ocho pines del chip SPI.

El chip SPI está situado cerca de los puertos SATA, justo al lado del mSATA. Busca el chip cuadrado etiquetado como "JMB575" — ese es el controlador SATA. Junto a él, encontrarás un chip de 8 pines más pequeño etiquetado como "W25X40CL", que es el chip SPI. La etiqueta del chip SPI puede ser difícil de leer, pero una vez que hayas localizado el controlador SATA, debería ser fácil identificar el chip SPI.

#### 2.1 Conectar el clip

Pin 1 en el clip está codificado por color en el cable — el cable rojo lo indica. El cable rojo debe enfrentarse al borde de la placa donde se encuentran los puertos de SATA.
Asegúrese de que el clip está completamente insertado. Si está conectado correctamente, debería ser capaz de levantar el tablero usando el clip.

Conecte el otro extremo del cable al parpadeo. La orientación correcta es la siguiente: si el conector USB del flasheador está apuntando lejos de ti, el cable debe entrar en los cuatro orificios superiores, con el cable rojo en la esquina inferior derecha.

#### 2.2 O desmayado el chip SPI

Toca un poco de mecha de soldar y flujo, calienta tu hierro, y desmayas la ficha. ¡Deberías saber lo que estás haciendo!

Entonces puede soldar la ficha directamente sobre el flasher (hay una almohadilla en la parte posterior del flasheador para esto), o utilice una de las tarjetas de adaptador incluidas en el paquete mencionado anteriormente.

Pin 1 está marcado en la ficha con un punto pequeño y está etiquetado con un "1" en la placa de flasher o adaptador.

### 3. Parpadear firmware

Primero necesita instalar flashrom.

```
sudo pacman -S flashrom
```

#### 3.1 Firmware de copia de seguridad

Antes de empezar a flashear una nueva rom es una buena idea para respaldar la roma existente. Siempre que algo va mal puedes volver con este archivo


