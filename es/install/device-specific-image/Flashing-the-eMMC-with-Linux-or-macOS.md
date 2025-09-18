---
title: Flashear el eMMC con Linux o macOS
description:
published: false
date: 2025-09-16T06:29:26.865Z
tags:
editor: markdown
dateCreated: 2025-09-16T06:29:26.865Z
---

# 1. Introducción

Esta guía describe cómo flashear un eMMC usando la herramienta `rkdeveloptool`. Se puede encontrar en la mayoría de los repositorios de Linux y también se ejecuta en macOS.

Para la instalación de BredOS, se requieren tres cosas:

1. Archivo de cargador SPI, por ejemplo para el RK3588: [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. Imagen específica del dispositivo de nuestro [sitio web oficial](https://bredos.org/download.html)
3. `rkdeveloptool`

# 2) Instalación

La instalación de `rkdeveloptool` se puede realizar con los siguientes pasos.

## 2.1 Linux

- Si está utilizando una distribución basada en arco

```
sudo pacman -S rkdeveloptool
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