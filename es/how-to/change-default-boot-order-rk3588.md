---
title: Cómo cambiar la orden de inicio predeterminada en RK3588
description: Aprenda cómo cambiar el orden de arranque por defecto en dispositivos basados en RK3588 usando la configuración del firmware UEFI
published: true
date: 2025-02-23T15:45:23.760Z
tags:
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 🔄 Cambiando la orden de inicio predeterminada en dispositivos RK3588

Si necesita modificar el orden de arranque en un dispositivo basado en RK3588 ejecutando BredOS, siga estos pasos:

---

## 🔹 Acceder al menú de Arranque UEFI

1. **Enciende tu consola** y espera a que aparezca el **logo** de BredOS durante el arranque.
2. **Presiona la tecla `ESC` una vez** mientras el logo se muestra para entrar en el menú UEFI.

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

---

## 🛠️ Navegando a los ajustes de orden de inicio

1. Usa las **teclas de flecha (`is` y `iso`)** para seleccionar **Gerente de Mantenimiento de Arrancamiento** y presiona **Enter**.\
   ![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

2. En la siguiente pantalla, seleccione **Opciones de Arrancamiento** y pulse **Intro**.

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

3. Elige **Cambiar orden de arranque** y presiona **Entrar**.

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

---

## 🔧 Modificando la Orden de Arranque

1. Una vez dentro del menú de orden de arranque, **presione Enter**.

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

2. Usa la **flecha hacia abajo (`mañana`)** para desplazarte hacia la parte inferior de la lista.

3. Selecciona la entrada que quieres mover a la parte superior y presiona la tecla **`+`** hasta que llegue a la parte superior.\
   ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)\
   ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

4. Una vez establecido el orden de arranque deseado, presione **Enter** para confirmar.

---

## 💾 Guardando y Aplicando los Cambios

1. Después de configurar el orden de arranque, presione **`Y`** para guardar los cambios.

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

2. Salga del menú y **reinicie el dispositivo** para aplicar el nuevo orden de arranque.

---

✅ **¡Hecho!** Tu consola ahora arrancará usando el nuevo orden. 🚀
