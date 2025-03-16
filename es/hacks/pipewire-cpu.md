---
title: Pipewire CPU puede solucionar
description: null
published: true
date: 2025-03-16T16:17:09.241Z
tags: null
editor: markdown
dateCreated: 2025-03-16T16:17:09.241Z
---

# Uso de Pipewire CPU

¿Se está comiendo una de tus úlceras sin motivo de nuevo?

Bueno, lo mejor que puedes hacer ahora es limitar su uso con `systemd`.

### Paso 1:

Crea el archivo `~/.config/systemd/user/pipewire.service` y coloca los siguientes datos dentro de él:

```
[Unit]
Description=PipeWire Multimedia Service

# Necesitamos pipewire. octén para estar activo antes de iniciar el daemon, ya que
# mientras es posible usar el servicio sin el socket, no está claro
# por qué podría ser.
#
# Un usuario instalando pipewire y haciendo `systemctl --user start pipewire`
# no iniciará el socket, que podría ser confuso y problemático si
# el servidor será reiniciado más adelante, como la característica de autoaparición del cliente
# podría entrar. Además, un inicio de la unidad de socket fallará, añadiendo a
# confusión.
#
# Después=pipewire. ocket no es necesario, ya que ya está implícito en la relación
# socket-service, vea systemd.socket(5).
Requires=pipewire. ocket

[Service]
CPUAccounting=true
CPUQuota=10%
LockPersonality=yes
MemoryDenyWriteExecute=yes
NoNewPrivileges=yes
RestrictNamespaces=yes
SystemCallArchTechntures=native
SystemCallFilter=@system-service
Type=simple
ExecStart=/usr/bin/pipewire
Restart=on-failure
Slice=session. cuadros

[Install]
Also=pipewire.socket
WantedBy=default.target
```

### Paso 2:

Guardar el archivo y ejecutar: `systemctl --user daemon-reload`

### Paso 3:

Cerrar sesión o reiniciar idealmente. Pipewire sólo utilizará el 10% de un solo núcleo como máximo. **No reinicie pipewire manualmente.**

Este hack no debe afectar a tu audio.
Si desea permitirle más margen de maniobra, cambie el porcentaje en la línea `CPUQuota`.