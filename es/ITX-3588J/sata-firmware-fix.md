---
title: Arreglo de firmware de Sata
description:
published: false
date: 2025-09-12T10:43:12.362Z
tags:
editor: markdown
dateCreated: 2025-09-12T09:18:06.486Z
---

# Arreglo de firmware SATA

## 1. Prerrequisitos

- Un flasheador basado en CH341
- Un soldado o un clip SPI
- El nuevo archivo de firmware (descargalo desde [here](/wiki-itx3588j-pics/satafw/sata_adapter_en25f40.bin))
- Otro dispositivo con Linux instalado (Windows debería funcionar también, pero no está cubierto aquí)

Un paquete muy práctico que incluye el flasher, el clip y otros accesorios útiles puede ser pedido aquí:
https://www.aliexpress.com/item/32263275388.html
![spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> Si el enlace ha caducado, siéntete libre de darnos una cabecera en Discord o Telegram.

## 2. Conectar a SPI

> ⚡ _Antes de conectar cualquier cosa a la potencia, ¡comprueba que todos los conectores estén correctamente orientados!_ ⚡
> {.is-warning}

La forma más sencilla de conectarse al chip SPI es usando el clip. Puede ser un poco complicado conseguir una conexión firme, pero no requiere ninguna habilidad de soldadura o herramientas. Además, es muy poco probable que el uso del clip cause algún daño en el foro.

Por otro lado, si tienes experiencia de soldadura, no es una tarea difícil desenvejecer y resolver los ocho pines del chip SPI.

El chip SPI está situado cerca de los puertos SATA, justo al lado del mSATA. Busca el chip cuadrado etiquetado como "JMB575" — ese es el controlador SATA. Junto a él, encontrarás un chip de 8 pines más pequeño etiquetado como "W25X40CL", que es el chip SPI. La etiqueta del chip SPI puede ser difícil de leer, pero una vez que hayas localizado el controlador SATA, debería ser fácil identificar el chip SPI.
![sata-controller-text-scaled.jpg](/wiki-itx3588j-pics/sata-controller-text-scaled.jpg)

### 2.1 Conectar el clip

Pin 1 en el clip está codificado por color en el cable — el cable rojo lo indica. El cable rojo debe enfrentarse al borde de la placa donde se encuentran los puertos de SATA.
Asegúrese de que el clip está completamente insertado. Si está conectado correctamente, debería ser capaz de levantar el tablero usando el clip.
![spi-clip-connected-cut.jpg](/wiki-itx3588j-pics/spi-clip-connected-cut.jpg)

Conecte el otro extremo del cable al parpadeo. La orientación correcta es la siguiente: si el conector USB del flasheador apunta hacia ti, el cable debe entrar en los cuatro orificios inferiores, con el cable rojo en la esquina superior izquierda.
![flasher-clip-connected-cut-scaled.jpg](/wiki-itx3588j-pics/flasher-clip-connected-cut-scaled.jpg)

### 2.2 O desmayado el chip SPI

Toca un poco de mecha de soldar y flujo, calienta tu hierro, y desmayas la ficha. ¡Deberías saber lo que estás haciendo!

Entonces puede soldar la ficha directamente sobre el flasher (hay una almohadilla en la parte posterior del flasheador para esto), o utilice una de las tarjetas de adaptador incluidas en el paquete mencionado anteriormente.
Debe haber una placa no poblada y un conector ZIF como parte del paquete. Elija sabiamente.

Pin 1 está marcado en la ficha con un punto pequeño y está etiquetado con un "1" en la placa de flasher o adaptador.
![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)
o
![spi-soldered-cut.jpg](/wiki-itx3588j-pics/spi-soldered-cut.jpg)

### 2.3 Comprobar conexión

Primero necesita instalar flashrom.

```
# sudo pacman -S flashrom
```

Comprueba todos los cables y asegúrate de que tu tablero ITX-3588J esté desconectado de la corriente si estás usando el clip.
Después, conecte el flasher a su dispositivo Linux y ejecute el siguiente comando.
Si reporta el nombre del chip SPI mencionado anteriormente, es bueno que vayas.

```
# sudo flashrom -p ch341a_spi --flash-name
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) en Linux 6.15.7-1-BredOS (x86_64)
flashrom es software libre, obtenga el código fuente en https://flashrom. rg

Utilizando clock_gettime para bucles de retraso (clk_id: 1, resolution: 1ns).
Se encontró el chip de flash Winbond "W25X40" (512 kB, SPI) en ch341a_spi.
```

Si no lo hace, compruebe la conexión de su clip o inspeccione su trabajo de soldadura, y verifique la orientación de todos los conectores.

## 3. Parpadear firmware

### 3.1 Copia de seguridad del viejo firmware

Antes de flashear una nueva ROM, es una buena idea hacer una copia de seguridad de la existente.
Si algo sale mal, podrás restaurarlo usando esta copia de seguridad.

Volcar el flash con el siguiente comando:

```
# sudo flashrom -p ch341a_spi -r firmware_dump.bin
```

Luego, volcarlo de nuevo y compare los dos archivos para asegurar que los datos se transfirieron correctamente.

```
# sudo flashrom -p ch341a_spi -r firmware_dump-1.bin
# diff firmware_dump.bin firmware_dump-1.bin
```

Si "Difier" no produce salida, es bueno que vayas.
Si lo hace, compruebe la conexión de su clip o inspeccione su trabajo de soldadura, y verifique la orientación de todos los conectores.

### 3.2 Flash nuevo firmware

Tan simple como el título sugiere:

```
# sudo flashrom -p ch341a_spi -w sata_adapter_EN25F40.bin 
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) en Linux 6.15. -1-BredOS (x86_64)
flashrom es software libre, obtenga el código fuente en https://flashrom.org

Usando clock_gettime para bucles de retraso (clk_id: 1, resolución: 1ns).
Se encontró el chip de flash Winbond "W25X40" (512 kB, SPI) en ch341a_spi.
===
Esta parte de flash tiene estado UNTESTADO para las operaciones: WP
El estado de prueba de este chip puede haber sido actualizado en la última versión de desarrollo
de flashrom. Si está ejecutando la última versión de desarrollo,
por favor envíe un informe a flashrom@flashrom. rg si alguna de las operaciones anteriores
funciona correctamente para usted con este chip flash. Por favor incluya el archivo de registro de flashrom
para todas las operaciones que ha probado (ver la página de manual para más detalles), y mencionar
que placa principal o programador ha probado en la línea de sujetos.
¡Gracias por tu ayuda!
Leyendo el viejo contenido de chip flash... hecho.
Borrar/escribir hecho de 0 a 7ffff
Verificando flash... VERIFIED.
```

Si ve el texto "VERIFICADO", el firmware ha sido instalado correctamente. Si usaste el clip, simplemente desconectalo y estarás listo para empezar. Si usted desmayó el chip, usted sabe qué hacer.

> 🍊 Este artículo de la wiki fue creado en un Orange Pi 5 Plus. 🍊
> {.is-success}
