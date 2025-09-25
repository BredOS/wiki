---
title: Administrar contenedores con systemd-nspawn
description:
published: false
date: 2025-09-25T10:15:56.522Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🎛️ 1. 📥 Instalar el Firmware

`systemd-nspawn` es una herramienta de contenedor ligera que viene con systemd, diseñada para ejecutar un entorno de comandos u sistema operativo en un entorno fuertemente aislado. A menudo descrito como "chroot en esteroides, proporciona una manera conveniente de probar o ejecutar distribuciones completas de Linux o entornos mínimos de una manera segura y controlada.

A diferencia de soluciones de virtualización completas como QEMU o plataformas contenedoras como Docker, `systemd-nspawn` utiliza espacios de nombres y grupos de Linux para crear contenedores con muy poca sobrecarga.

# 3. Crear plantilla de contenedor

Los contenedores que usan nspawn pueden ejecutarse desde cualquier ubicación en tu sistema de archivos, pero la carpeta recomendada es `/var/lib/machines`. Dentro de esta carpeta, creamos una subcarpeta que contiene nuestras raíces Linux/GNU. Para simplificar el proceso, este artículo le guía a través de la creación de una plantilla de contenedor. El contenido de esa carpeta de plantillas puede ser copiado a una nueva ubicación y usado como un nuevo entorno de contenedor.

- Cambiar a tu usuario root:

```
sudo su
```

- Luego cambie el directorio a `/var/lib/machines`:

```
cd /var/lib/máquinas
```

- Y crear una carpeta de plantilla:

```
plantilla mkdir
```

Como un contenedor puede contener cualquier distribución de rootfs, usted es relativamente libre en su elección. Proporcionamos una lista de tarball de distribución mínima, como Debian, Ubuntu y BredOS; Sin embargo, tenga en cuenta que este artículo es específicamente para un contenedor BredOS.

> Cualquier comando que necesite ser ejecutado dentro de su contenedor debe ser ajustado de acuerdo a la variante de su distribución si no está usando BredOS.
> {.is-info}

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) Busca la liberación de tu elección y luego descarga el `.tar.gz` para la arquitectura de tu CPU.
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) Desplácese hacia abajo y haga clic en la versión que desea descargar, luego descargue el `.tar.gz` para su arquitectura de CPU.
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) Scroll down and choose between `Container Base` or `Container Minimal Base`.
- [Arch Linux](https://archlinux.org/download/) Elige una réplica cerca de ti, luego descarga el archivo `.tar.zst`.
- [Arch Linux ARM](https://archlinuxarm.org/os/) Descarga el archivo .tar.gz con la etiqueta `latest` y `aarch64` o `armv7`.
  {.links-list}

> ¡Pronto estará disponible un Rootfs BredOS!
> {.is-warning}

Después de descargar el tarball rootfs elegido, necesita ser extraído. En este ejemplo, hemos descargado el tarball Arch Linux ARM y lo hemos convertido en BredOS.

- Todavía como root extrae el tarball en `/var/lib/machines/template`:

```
tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- El contenido de la carpeta `template` debe verse así:

```
ls template/
bin boot dev etc home lib mnt opt proc root run sbin srv sys tmp usr var
```

- Para introducir el contenedor, ejecutar:

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template
```

El parámetro `--machine` define el nombre del contenedor, mientras que `--directory` apunta a la ubicación del contenedor. Para salir del contenedor, usa <kbd>Ctrl</kbd> + <kbd>D</kbd> o escribe <kbd>Ctrl</kbd> + <kbd>]</kbd> tres veces en un segundo.

Lo primero que queremos hacer dentro del contenedor es inicializar nuestro gestor de paquetes y actualizar el sistema.

- Para hacer esto, ejecutar:

```
pacman-key --init
pacman-key --populate
pacman -Syu
```

> Si encuentra problemas al resolver nombres de host, elimine el archivo `/var/lib/machines/templateň/resolv.conf` del sistema host.
> {.is-info}

- Después de esto necesitamos eliminar algunas cosas innecesarias como el núcleo y firmware:

```
pacman -R linux-aarch64 linux-firmware
```

- Para convertir el contenedor a BredOS, ejecute lo siguiente:

```
pacman-key --recv-keys 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
pacman-key --lsign-key 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
echo -e '# --> BredOS Mirrorlist <-- #\n\n# BredOS Main mirror\nServer = https://repo.bredos.org/repo/$repo/$arch\n' | tee /etc/pacman.d/bredos-mirrorlist
```

- Luego edite el archivo de réplica:

```
nano /etc/pacman.conf
```

- And add the following to the end of the file:

```
[BredOS-any]
Incluya = Ninguno/pacman.d/bredos-mirrorlist

[BredOS]
Incluido = Ninguno/pacman.d/bredos-mirrorlist
```

Save and close the file with <kbd>Ctrl</kbd> + <kbd>X</kbd> and <kbd>Y</kbd>

- Finalmente iniciar la conversión con:

```
pacman -Syu bred-os-release BredOS-any/lsb-release bredos-logo
```

- Opcionalmente, instalar bredos-config y/o bredos-news:

```
pacman -Sy bredos-config bredos-news
```

# 4. Ejecutar contenedor con red virtual

El contenedor que hemos creado en la sección [2. Crear plantilla de contenedor](#h-3-create-container-template) usó la red de su sistema de host. If you prefer a virtual network device on your container, for example if you want to use [Open vSwitch](/how-to/open-vswitch), do the following.

- Si desea hacer esto en un nuevo contenedor, clónelo:

```
mkdir /var/lib/machines/template-veth
rsync -avP /var/lib/machines/template/* /var/lib/machines/template-veth/
```

> Para simplificar esta guía continuaremos trabajando con nuestra plantilla creada en [2. Crear plantilla de contenedor](#h-3-create-container-template).
> {.is-info}

- Primero, introduzca el contenedor como antes:

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template
```

Para mantener el tema systemd, usamos `systemd-networkd` para configurar nuestro dispositivo de red virtual.

- Crear dos archivos de configuración con:

```
táctil, /systemd/network/80-container-host0.network
nano /etc/systemd/network/99-wolVeth.network
```

- Pegue lo siguiente en el archivo de configuración:

```
[Match]
Nombre=host0

[Network]
Dirección=<containers ip address> ejemplo -> 192.168.1.100/24
Gateway=<gateway of that network> ejemplo -> 192.168. .1
DNS=<DNS Servers address> ejemplo -> 9.9.9.9
#DHCP=yes -> o dirección de comentarios, Gateway y DNS y descomentar DHCP para asignar la dirección automáticamente
```

- Finalmente, habilitar `systemd-networkd`:

```
systemctl habilitar systemd-networkd
```

To let the container start that service, it needs to be booted (the previous command is more like chrooting). We achieve this by using the `--boot` parameter. Additionally, we add the `--network` parameter to start the container with a virtual network device.

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template --boot --network
```

This will boot the container and display the login prompt. Logging in as root is not possible, so you must either create a user before booting into the container or proceed to section [4. Ejecutar contenedor como servicio](#h-4-run-container-as-a-service).

- Para crear un usuario, ejecute lo siguiente dentro de su contenedor:

```
useradd <your username here>
passwd <your username here>
```

> Como tal vez quiera utilizar su dispositivo de red virtual para el trabajo real en red, se necesita más configuración. Use, por ejemplo, [Abrir vSwitch](/how-to/open-vswitch) o un simple dispositivo puente para conectar el dispositivo de red virtual a algo.
> {.is-info}

# 5. Ejecutar contenedor como un servicio

Es posible iniciar un contenedor como un servicio, por ejemplo para iniciarlo en tiempo de arranque. Hay una implementación a través de la unidad systemd-nspawn@.service, pero requiere crear archivos de sobreescritura para configurarlo. Nuestra forma preferida es crear un nuevo fichero de servicios, el cual contiene todos los parámetros que queremos utilizar para nuestro contenedor.

- Clone the template to create a new container:

```
mkdir /var/lib/machines/my-first-container
rsync -avP /var/lib/machines/template/* /var/lib/machines/my-first-container/
```

- Luego crea un nuevo archivo de servicios en tu host con:

```
sudo nano ► /systemd/<your containers name here>.service
```

- Y pega lo siguiente en él:

```
[Unit]
Description=<your containers name here>
After=network.target
Requires=red.

[Service]
ExecStart=/usr/bin/systemd-nspawn --machine=<your containers name here> --directory=/var/lib/machines/my-first-container --boot
KillMode=mixed
Type=notify
Restart=always

[Install]
WantedBy=multi-user. Objetivo

```

If you want to use a virtual network device on your container add, `--network` at the end of `ExecStart=/usr/...`.

- Luego puede iniciar el contenedor con:

```
sudo systemctl iniciar <your containers name here>.service
```

- O dejar que empiece en tiempo de arranque con:

```
sudo systemctl habilita <your containers name here>.service
```

- Para iniciar sesión en tu contenedor, usa `machinectl`:

```
la shell de sudo machinectl <your containers name here>
```

- Y compruebe todos los contenedores en ejecución (y VM's) con:

```
maquinaria de sudo
```

# 4. Acceder a archivos/carpetas en el host desde dentro del contenedor

As the name suggests, a container typically does not have access to your host system. This can be modified to allow the container access to specific files or folders on your host system; for example, to provide additional storage space or grant the container access to your GPU.

- Access to a file/folder can be achieved with the `--bind` parameter:

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template --bind=<path to your location>
```

- Por ejemplo, si desea compartir su floder de inicio:

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template --bind=/home
```

This will mount the folder `/home` to the same location within your container. If you wish to change the mount point inside your container, you can specify this by using a <kbd>:</kbd> between both paths.

- Por ejemplo, si quieres `/home` en `/tmp/home`:

```
systemd-nspawn --machine="Plantilla" --directory=/var/lib/machines/template --bind=/home:/tmp/home
```

# 8. Notas adicionales

`systemd-nspawn` es una herramienta extremadamente potente. What we covered here are just the basics. Echa un vistazo a la [página de manual](https://www.freedesktop.org/software/systemd/man/latest/systemd-nspawn.html), si quieres estar asombroso!