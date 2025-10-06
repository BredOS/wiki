---
title: Flashear el eMMC con Linux o macOS
description:
published: true
date: 2025-09-29T06:00:19.076Z
tags:
editor: markdown
dateCreated: 2025-09-16T06:29:26.865Z
---

# 1. Introducción

Esta guía describe cómo flashear un eMMC usando la herramienta `rkdeveloptool`. Se puede encontrar en la mayoría de los repositorios de Linux y también se ejecuta en macOS.

Para la instalación de BredOS, se requieren tres cosas:

1. Archivo del cargador SPL, por ejemplo para el RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

### Tabset {.tabset}

#### RK3588

[`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

#### RK3566

\
Por ejemplo, para el RK3566, el cargador SPL se puede encontrar aquí:
[`rk356x_spl_loader_ddr1056_v1.10.111.bin`](https://dl.radxa.com/rock3/images/loader/rock-3a/rk356x_spl_loader_ddr1056_v1.10.111.bin)
{.is-info}

###

2. Imagen específica del dispositivo de nuestro [sitio web oficial](https://bredos.org/download.html)
3. `rkdeveloptool`

> Proporcionamos nuestras imágenes como archivos comprimidos .xz. ¡Necesita extraer el archivo .img que contiene antes de flashear!
> {.is-warning}

# 3. Parpadeando

La instalación de `rkdeveloptool` se puede realizar con los siguientes pasos.

## 2.1 Linux

- Si está utilizando una distribución basada en arco

```
sudo pacman -S rkdeveloptool-git
```

- Si está utilizando una distribución basada en Debian

```
sudo apt instalar rkdeveloptool
```

- Si está utilizando una distribución basada en Red Hat

```
sudo dnf instalar rkdeveloptool
```

## 2.2 macOS

### 2.2.1 Prerrequisitos

Como no hay ningún paquete binario para `rkdeveloptool` para macOS, necesitamos compilarlo nosotros mismos. Para ello, necesitamos tener algunos paquetes instalados a través de [Brew](https://brew.sh/).

- Instala `automake`, `autoconf`, `libusb`, `pkg-config`, `git` y `wget` con el siguiente comando:

```
brew install automake autoconf libusb pkg-config git wget
```

### 2.2.2 Clonar repositorio

- Obtener el código fuente con:

```
git clone https://github.com/rockchip-linux/rkdeveloptool
```

### 2.2.3 Compilar al binario

- Ahora cambie al directorio que contiene el código fuente y lo complique:

```
cd rkdeveloptool
autoreconf -i
./configure
make -j $(nproc)
```

- Después de que el proceso `make` haya terminado sin un error hay el archivo `rkdeveloptool` dentro de tu carpeta actual:

```
ls | grep rkdeveloptool
```

- debe salir

```
rkdeveloptool
```

### 2.2.4 Ejecutar

- Y finalmente cópialo en la carpeta `opt` para ejecutarlo desde todas partes:

```
cp rkdeveloptool /opt/homebrew/bin/
```

# 3. Parpadeando

## 3.1 Introducir máscara

Para que el SBC aparezca como un dispositivo flasheable sobre el USB, necesita configurarse en `modo maskrom`. Esto puede lograrse de forma diferente dependiendo del dispositivo que esté utilizando. Algunos SBCs tienen un botón, mientras que otros requieren que corres dos pinchos. Consulte la documentación de su fabricante SBC.

- Esta información se puede encontrar fácilmente con una búsqueda de Google:

```
Modo maskrom <your sbcs name here>
```

- Para verificar que tu dispositivo está en el modo 'maskrom' y ha sido correctamente descubierto por tu PC, ejecutado:

```
sudo rkdeveloptool ld
```

- Si ves lo siguiente, es bueno ir (la salida es similar, pero no idéntica):

```
DevNo=1 Vid=0x2207,Pid=0x350b,LocationID=801 Maskrom
```

> El botón de Maskrom se debe mantener presionado **mientras se conecta la energía** en el tablero.
> {.is-info}

> El uso de cables USB-C a C, o de un cable USB-C a un cable hacia atrás puede resultar en que no se detecte la placa.
> Se recomienda usar un cable USB-C a un cable, luego una [USB-C Femenina al adaptador USB-A Masal](https://www.aliexpress.com/item/1005004767752226.html) o un cable USB-A.
> {.is-warning}

## 3.2 Flash BredOS

Ahora que somos capaces de enviar comandos al dispositivo con `rkdeveloptool`, vamos a hacer un SBC BredOS de él.

- Enviar el archivo de cargador SPI a su SBC:

```
sudo rkdeveloptool db <path to SPI loader file here>
```

- A continuación, escriba la Imagen Específica del dispositivo BredOS en su eMMC:

```
sudo rkdeveloptool wl 0 <path to BredOS image here>
```

- Y finalmente reinicie su dispositivo:

```
sudo rkdeveloptool rd
```

> Después de flashear con éxito, proceda con [**Primera configuración**](/en/install/first-setup).
> {.is-success}

# 5. Información adicional

Bueno, sólo quieres más barras de progreso en tu vida, ¿verdad? Te hemos cubierto, no te preocupe.

## 4.1 Leyendo información del medio de flash elegido

El comando `sudo rkdeveloptool rfi` te mostrará los detalles del medio de flash elegido.

- De forma predeterminada, esto normalmente es el eMMC, a menos que no esté disponible.

```
Información Flash:
	Fabricante: SAMSUNG, value=00
	Tamaño Flash: 14910 MB
	Tamaño Flash: 30535680 Sectores
	Tamaño del bloque: 512 KB
	Tamaño de la página: 2 KB
	Bits de la ECC: 0
	Tiempo de acceso: 40
	Flash CS: Flash<0>
```

## 4.2 Cambiando objetivo flash

¿Quieres flash / volcar no el eMMC sino una cosa diferente?

- `sudo rkdeveloptool cs 2` para elegir la tarjeta sdcard.
- `sudo rkdeveloptool cs 9` para seleccionar el chip SPINOR.
- `sudo rkdeveloptool cs 1` para seleccionar el eMMC de nuevo.

El cambio se reflejará en `sudo rkdeveloptool rfi`.