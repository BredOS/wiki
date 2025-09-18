---
title: Pipewire CPU puede solucionar
description:
published: true
date: 2025-09-17T09:24:40.286Z
tags:
editor: markdown
dateCreated: 2025-03-16T16:17:09.241Z
---

# 1. Introducción

¿Se está comiendo una de tus úlceras sin motivo de nuevo?

Bueno, lo mejor que puedes hacer ahora es limitar su uso con `systemd`.

# 2. Limitar cuota de CPU

## 2.1 Crear archivo de servicio:

- Crea el archivo `~/.config/systemd/user/pipewire.service` y coloca los siguientes datos dentro de él:

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

## 2.2 Recargar daemon del sistema

- Guardar el archivo y ejecutar:

```
systemctl --daemon-recargar usuario
```

## 2.3 Cerrar sesión o reiniciar:

Cerrar sesión o reiniciar idealmente. Pipewire sólo utilizará el 10% de un solo núcleo como máximo.

> No reinicie pipewire manualmente.
> {.is-warning}

Este hack no debe afectar a tu audio.
Si desea permitirle más margen de maniobra, cambie el porcentaje en la línea `CPUQuota`.