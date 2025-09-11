---
title: Cómo ejecutar máquinas virtuales en BredOS
description:
published: true
date: 2024-10T22:18:35.474Z
tags: vm, cómo hacer
editor: markdown
dateCreated: 2024-05T22:12:39.679Z
---

# 🚀 Ejecutar máquinas virtuales con Virt-Manager en BredOS

Esta guía le ayudará a configurar y administrar máquinas virtuales usando `virt-manager` en BredOS.

## 📋 Prerrequisitos

Antes de comenzar, asegúrese de tener lo siguiente:

- Una conexión de internet funcional 🌐
- Privilegios Sudo 🔑

## Paso 1: Instalar paquetes requeridos 📦

Para empezar, necesita instalar los paquetes necesarios para KVM y `virt-manager`.

```bash
sudo pacman -Syu
sudo pacman -S virt-manager virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

## Paso 2: Activar e iniciar el servicio Libvirt

Una vez instalados los paquetes, habilite e inicie el servicio `libvirtd`:

```bash
sudo systemctl habilitar --now libvirtd
```

Para verificar que el servicio está en ejecución:

```bash
sudo systemctl status libvirtd
```

## Paso 3: Añade tu usuario al grupo `libvirt` 👥

Para evitar necesitar privilegios de root para administrar máquinas virtuales, añade tu usuario al grupo `libvirt`:

```bash
sudo usermod -aG libvirt $(whoami)
```

Después de añadirte al grupo, cierra sesión y vuelve a iniciar sesión para que los cambios surtan efecto.

## Paso 4: Configurar red 🌐

`virt-manager` usa `dnsmasq` para la gestión de red. Puede que desee asegurarse de que `libvirt` está configurado con los ajustes de red predeterminados:

```bash
sudo virsh net-start predeterminado
predeterminado de virsh net-autostart
```

## Paso 5: Iniciar Virt-Manager 🖥️

Ahora que todo está configurado, puedes iniciar `virt-manager`:

```bash
virt-manager
```

Esto abrirá el GUI `virt-manager` donde puedes crear y administrar máquinas virtuales.
![virt.jpg](/vms/virt.jpg)

## Paso 6: Habilitar edición XML

Para habilitar la edición XML (se necesita más tarde) tienes que abrir `virt-manager` ir a **Editar** luego **Preferencias** y habilitar la edición XML
![xmlediting.jpg](/vms/xmlediting.jpg)

## Paso 7: Crear una máquina virtual 🛠️

1. Abrir `virt-manager`.
   ![virt.jpg](/vms/virt.jpg)
2. Haga clic en **Crear una nueva máquina virtual** ➕.
   ![virtnewvm.jpg](/vms/virtnewvm.jpg)
3. Seleccione el origen de la instalación (imagen ISO o instalación de red).
   ![newvm.jpg](/vms/newvm.jpg)
4. Siga el asistente para asignar CPU, RAM y almacenamiento para su VM. ⚙️

> En el RK3588 puedes asignar máximo 4 núcleos por vm debido a la pequeña arquitectura grande
> {.is-warning}

![disk.jpg](/vms/disk.jpg)
![cpuram.jpg](/vms/cpuram.jpg)
5. En CPUs con lo poco. La arquitectura ig como el RK3588 necesita comprobar "Personalizar configuración antes de instalar" y editar el xml responsable de asignar núcleos de cpu
![finalstep.jpg](/vms/finalstep. pg)
Haga clic en **Finalizar**
![vcpuxml0.jpg](/vms/vcpuxml0.jpg)
Abra la configuración de **CPUs** y luego la pestaña **XML**
![vcpuxml1.jpg](/vms/vcpuxml1. pg)
Localice `<vcpu>XYZ</vcpu>` y reemplácelo con

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

Donde el set de cpu son los núcleos que quieres usar 0-3 son los núcleos E en el rk3588 y 4-7 son los núcleos de rendimiento y el número de núcleos. En el ejemplo de arriba la vm tendrá 2 núms. con ellos es la eficiencia núm. 1 y 2 núm.
¡[vcpuxml2.jpg](/vms/vcpuxml2.jpg)

6. Añadir soporte para hardware periférico y gráficos. 🖥️

Diríjase a la página de la MV, presione "Añadir Hardware".

![addhw.png](/vms/addhw.png)

Luego, en la ventana que aparecerá seleccione "Video" y en la selección del modelo, seleccione "ramfb" y haga clic en "Finalizar".

![gpu.png](/vms/gpu.png)

Ahora para añadir el servidor de gráficos, selecciona "Añadir hardware" de nuevo, "Gráficos" y haz clic en "Finalizar".

![graphics.png](/vms/graphics.png)

Ahora para el teclado y el ratón, repita el mismo procedimiento seleccionando:
"Entrada" -> "Tabla USB de teclado"
y
"Entrada" -> "EvTouch USB Graphics Tablet"

![tab.png](/vms/kb.png)
![tab.png](/vms/tab.png)

7. Una vez configurado, inicie la máquina virtual. 🟢

![startvm.jpg](/vms/startvm.jpg)

## Configuración adicional ⚙️

- Para administrar máquinas virtuales a través de línea de comandos, puede utilizar `virsh`:

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

## Solución de problemas 🛠️

- **Problemas de permiso**: Asegúrate de que tu usuario está en el grupo `libvirt` y que el servicio `libvirtd` se está ejecutando.
- **Problemas de red**: Si las máquinas virtuales no tienen acceso a Internet, asegúrese de que la red `virsh` por defecto está en ejecución.

## 🎉 Conclusión

¡Has configurado con éxito `virt-manager` en BredOS y estás listo para crear y administrar máquinas virtuales!
