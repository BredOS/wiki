---
title: Contraseña GRUB
description: Asegurando GRUB con una contraseña
published: true
date: 2025-05-05T17:13:59.940Z
tags: null
editor: markdown
dateCreated: 2025-05-05T17:13:14.153Z
---

# 🔐 Protección de contraseña GRUB

BredOS incluye una utilidad para restringir las opciones de arranque GRUB con una contraseña.
Esto evita que los usuarios no autorizados inicien entradas no predeterminadas o editen parámetros de arranque.

# 🟢 Activar contraseña GRUB

`sudo grub-password`

Se te pedirá que introduzcas y confirmes una contraseña.
Una vez establecido, sólo la entrada GRUB por defecto puede iniciarse sin autenticación.

# 🔴 Desactivar contraseña GRUB

`sudo grub-password -d`

Esto elimina la restricción de contraseña y restaura el comportamiento normal de GRUB.

## Notas

La configuración se almacena en src/grub.d/99-bredos-grub-password.
El script regenera la configuración GRUB automáticamente mediante grub-mkconfig.