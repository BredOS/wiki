---
title: Cómo administrar interruptores virtuales
description:
published: true
date: 2025-09-25T06:12:54.789Z
tags:
editor: markdown
dateCreated: 2025-09-24T11:30:44.31Z
---

# 🎛️ 1. 📥 Instalar el Firmware

Open vSwitch (OVS) es un interruptor virtual de código abierto y de varias capas diseñado para permitir la automatización avanzada de la red al mismo tiempo que soporta interfaces y protocolos de gestión estándar. Se utiliza principalmente en entornos virtualizados para facilitar la comunicación entre máquinas virtuales (MVs), así como entre máquinas virtuales y la red física.

# 3. Instalación

- Se puede instalar OVS ejecutando este comando:

```
sudo pacman -S openvswitch
```

- Después de la instalación exitosa, necesitamos habilitar e iniciar el servicio OVS:

```
sudo systemctl habilitar --now ovs-vswitchd
```

# 4. Crear un vSwitch

OVS y sus conmutadores pueden ser gestionados con la herramienta `ovs-vsctl`.

- Para crear un nuevo conmutador ejecutar:

```
sudo ovs-vsctl add-br <your switch name here>
```

Por favor, reemplaza `<your switch name here>` con un nombre de tu elección.

# 5. Conectar dispositivos de red virtual

## 4.1 manualmente

Los dispositivos de red virtual pueden ser creados manualmente, a través de su hipervisor, o a través de un contenedor. Aparecerán y funcionarán como dispositivos físicos de red.

- Para listar todos los dispositivos de red ejecutar:

```
ip a
```

- Con la salida de ejemplo abajo podemos ver tres dispositivos:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp49s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master ovs-system state UP group default qlen 1000
    link/ether 00:48:54:20:41:e0 brd ff:ff:ff:ff:ff:ff
    altname enx0048542041e0
    inet6 fe80::248:54ff:fe20:41e0/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
3: ve-databaselCjq@if2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master ovs-system state UP group default qlen 1000
    link/ether 82:22:48:3a:2b:1a brd ff:ff:ff:ff:ff:ff link-netnsid 4
    altname ve-databaseserver.dmz
    inet 169.254.19.70/16 metric 2048 brd 169.254.255.255 scope link ve-databaselCjq
       valid_lft forever preferred_lft forever
    inet 192.168.244.177/28 brd 192.168.244.191 scope global ve-databaselCjq
       valid_lft forever preferred_lft forever
```

En este ejemplo, usamos `ve-databaselCjq`, que es un dispositivo de red virtual que fue generado desde un contenedor de nspawn del sistema.

- Para conectarlo a nuestro vswitch, ejecute:

```
sudo ovs-vsctl add-port <your switch name here> ve-databaselCjq
```

- Si quieres etiquetar los paquetes de ese adaptador a un vlan, usa el parámetro `tag`:

```
sudo ovs-vsctl add-port <your switch name here> ve-databaselCjq tag=<your vlan id tag here>
```

## 4.1 Automáticamente a través de libvirt

Si siguiste [esta guía](/how-to/run-vms) para crear la pila de hipervisor con qemu/libvirt, puede añadir su nuevo cambio a las redes conocidas por libvirt. Esto le permite seleccionar su vSwitch en la GUI, y el dispositivo de red virtual de su VM se añadirá automáticamente a ese vSwitch al arrancar.

- Inicia `virt-manager` y haz clic derecho en `QEMU/KVM`, que está marcado en azul en la captura de pantalla de abajo. Luego haga clic en «Detalles».

![main.png](/vswitch/main.png)

En la nueva ventana, cambia a la pestaña `Red Virtual`, y luego haz clic en el signo <kbd>+</kbd> en la esquina izquierda.

- Luego cambia a la pestaña `XML` y reemplaza el contenido con lo siguiente:

```
<network>
  <name><your switch name here></name>
  <forward mode='bridge'/>
  <bridge name='<your switch name here>'/>
  <virtualport type='openvswitch'/>
  <portgroup name='vlan-01' default='yes'>
  </portgroup>
  <portgroup name='vlan-02'>
    <vlan>
      <tag id='2'/>
    </vlan>
  </portgroup>
</network>
```

- Reemplaza `<your switch name here>` dos veces en la configuración dada. Con la etiqueta `portgroup`, puedes definir el vlan's que quieres usar en ese conmutador.

![network.png](/vswitch/network.png)

# 4. Conectar vSwitch a una red física

Si desea conectar su vSwitch a una red física, debe utilizar un dispositivo de red físico.

> Tenga en cuenta que el dispositivo de red usado **no** debe tener una dirección IP asignada!
> {.is-info}

- Para añadir `enp49s0` desde la salida de ejemplo anterior, ejecuta:

```
sudo ovs-vsctl add-port <your switch name here> enp49s0
```

Si solo tiene un dispositivo físico de red y/o quiere usarlo para la red de su dispositivo anfitrión, debe asignar una dirección IP al vSwitch en lugar del dispositivo de red físico. Esto se puede hacer utilizando cualquier herramienta; por ejemplo, con GUI del administrador de redes o a través del sistema.

# 8. Conecta dos vSwitches a través de Internet

Si tienes dos dispositivos conectados a través de VPN a través de Internet, es posible conectar sus vSwitches. Esto permite que los dispositivos en estos vSwitches se comuniquen entre sí sin más configuración. Si su vSwitch está conectado a un interruptor físico, es incluso posible conectar dispositivos físicos a través de ese túnel a través de Internet. Esto puede ser útil para muchos propósitos.

- Ejecutar lo siguiente en ambos hosts:

```
sudo ovs-vsctl add-port <your switch name here> vxlan0 -- establecer interfaz vxlan0 type=vxlan options:remote_ip=<IP address of other host>
```

Como siempre, reemplaza `<your switch name here>` con el nombre de tu interruptor, y `<IP address of other host>` con la dirección IP del host con la otra vSwitch. Eso; ahora sus dispositivos conectados pueden comunicarse de forma segura a través de Internet.

> Si sus clientes pueden hacer ping entre sí, pero la comunicación adicional no funciona, probablemente es un problema de MTU.
> {.is-danger}

## 6.1 Arreglar problema MTU

El MTU define el tamaño máximo de cada paquete transferido. Mientras que los paquetes ping normalmente no se llenan hasta este máximo, la comunicación "real" lo hace. El MTU por defecto es de 1500 bytes; si envía un paquete de ese tamaño a través de un túnel, el túnel mismo necesita agregar información como direcciones de origen y destino. Esto puede exceder el MTU, causando que el paquete sea dividido, lo que puede causar problemas para las comunicaciones de sus clientes. Para arreglar esto, simplemente reduzca el MTU para sus clientes a, por ejemplo, 1200 bytes. Este ajuste puede hacerse a través de su servidor DHCP o manualmente.

# 8. Comandos adicionales

- Para listar todos los dispositivos conectados de su vSwitch, ejecute:

```
sudo ovs-vsctl list-ports <your switch name here> 
```

- Para desconectar un dispositivo de red, ejecute:

```
sudo ovs-vsctl del-port <your switch name here> <your adapters name here>
```

