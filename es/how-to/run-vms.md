---
title: Ejecutar máquinas virtuales en BredOS
description:
published: true
date: 2025-09-17T10:43:46.119Z
tags: vm, cómo hacer
editor: markdown
dateCreated: 2024-05T22:12:39.679Z
---

# 1. Introducción

Esta guía le ayudará a configurar y administrar máquinas virtuales usando `virt-manager` en BredOS.

# 2. Prerrequisitos

Antes de comenzar, asegúrese de tener lo siguiente:

- Una conexión a Internet en funcionamiento
- privilegios de `sudo`

# 3. Instalación

## 3.1 Instalar paquetes requeridos

- Para empezar, necesita instalar los paquetes necesarios para `qemu` y `virt-manager`.

```
sudo pacman -Syu virt-manager virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

> Mientras que `qemu` es tu hipervisor, `virt-manager` es una herramienta basada en GUI para gestionarla.
> {.is-info}

## 3.2 Activar e iniciar el servicio Libvirt

- Una vez instalados los paquetes, habilite e inicie el servicio `libvirtd`:

```bash
sudo systemctl habilitar --now libvirtd
```

- Para verificar que el servicio está en ejecución:

```bash
sudo systemctl status libvirtd
```

## 3.3 Añade tu usuario al grupo `libvirt`

- Para evitar necesitar privilegios de root para administrar máquinas virtuales, añade tu usuario al grupo `libvirt`:

```bash
sudo usermod -aG libvirt $(whoami)
```

> Esto permite administrar máquinas virtuales desde el nivel de usuario. ¡Esto puede ser peligroso!
> {.is-warning}

- Después de añadirte al grupo, cierra sesión y vuelve a iniciar sesión para que los cambios surtan efecto.

## 3.4 Configurar red

- `virt-manager` usa `dnsmasq` para la gestión de red. Puede que desee asegurarse de que `libvirt` está configurado con los ajustes de red predeterminados:

```bash
sudo virsh net-start predeterminado
predeterminado de virsh net-autostart
```

## 3.5 Iniciar Virt-Manager

- Ahora que todo está configurado, puedes iniciar `virt-manager`:

```bash
virt-manager
```

- Esto abrirá el GUI `virt-manager` donde puedes crear y administrar máquinas virtuales.

![virt.jpg](/vms/virt.jpg)

> Si no has añadido tu usuario al grupo `libvirt` necesitas introducir tu contraseña ahora.
> {.is-info}

## 3.6 Activar edición de XML

- Para habilitar la edición XML (necesario posteriormente) necesitas abrir `virt-manager`, luego ve a `Edit` y luego a `Preferences` y `Activa la edición XML`.

# 4. Crear una máquina virtual

- Dentro de `virt-manager` haga clic en el icono de visualización o vaya a `File` -> `Crear máquina virtual` para crear una nueva máquina virtual.

- Seleccione el origen de la instalación (Local install media o Network Install).

- Si elige un medio de instalación local, utilice el asistente para seleccionar su archivo .is.

- Siga el asistente para asignar CPU, RAM y almacenamiento para su VM.

> En el RK3588 puede asignar máx. 4 núcleos por vm debido a la pequeña arquitectura grande.
> {.is-warning}

- Antes de hacer clic en `Finalizar` debes comprobar "**Personalizar configuración antes de instalar**" y editar el xml responsable de asignar núcleos de la CPU.

- Haz clic en `Finalizar`

Se abre una nueva ventana, que le permite editar la configuración de su máquina virtual antes de crearla. Abre la configuración de las CPUs y luego la pestaña XML

- Localiza `<vcpu>XYZ</vcpu>` y reemplazalo con

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

> Donde `cpu set` son los núcleos que quieres usar 0-3 son los núcleos E en el rk3588 y 4-7 son los núcleos de rendimiento y el número de núcleos. En el ejemplo de arriba la vm tendrá 2 núms. con ellos es la eficiencia núm. 1 y 2 núm.
> {.is-info}

- Una vez configurado, inicie la máquina virtual.

> Eso es lo que tenemos. ¡Ahora puedes correr Bred dentro de Bred!
> {.is-success}

# 5. Configuración adicional

- Para administrar máquinas virtuales a través de línea de comandos, puede utilizar `virsh`:

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

# 5. Solución de problemas

- **Problemas de permiso**: Asegúrate de que tu usuario está en el grupo `libvirt` y que el servicio `libvirtd` se está ejecutando.
- **Problemas de red**: Si las máquinas virtuales no tienen acceso a Internet, asegúrese de que la red `virsh` por defecto está en ejecución.

