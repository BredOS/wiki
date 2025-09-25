---
title: Manage systemd-nspawn containers
description:
published: false
date: 2025-09-25T10:54:42.662Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🎛️ 1. 📥 Installing the Firmware

`systemd-nspawn` is a lightweight container tool that comes with systemd, designed to run a command or OS environment in a tightly isolated environment. Often described as "chroot on steroids," it provides a convenient way to test or run entire Linux distributions or minimal environments in a secure and controlled manner.

Unlike full virtualization solutions like QEMU or container platforms like Docker, `systemd-nspawn` uses Linux namespaces and cgroups to create containers with very little overhead.

# 3. Create a container template

Containers using nspawn can be run from any location on your filesystem, but the recommended folder is `/var/lib/machines`. Inside this folder, we create a subfolder that holds our Linux/GNU rootfs. To simplify the process, this article guides you through creating a container template. The contents of that template folder can then be copied to a new location and used as a new container environment.

- Switch to your root user:

```
sudo su
```

- Then change directory to `/var/lib/machines`:

```
cd /var/lib/machines
```

- And create a template folder:

```
mkdir template
```

As a container can hold any distribution's rootfs, you are relatively free in your choice. We provide a list of minimal distribution tarballs, such as Debian, Ubuntu, and BredOS; however, please be aware that this article is specifically for a BredOS container.

> Any commands that need to be run inside your container must be adjusted according to your distribution's variant if you are not using BredOS.
> {.is-info}

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) Look up your release of choice, then download the `.tar.gz` for your CPU architecture.
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) Scroll down and click on the release you want to download, then download the `.tar.gz` for your CPU architecture.
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) Scroll down and choose between `Container Base` or `Container Minimal Base`.
- [Arch Linux](https://archlinux.org/download/) Choose a mirror near you, then download the `.tar.zst` file.
- [Arch Linux ARM](https://archlinuxarm.org/os/) Download the .tar.gz file with the `latest` and `aarch64` or `armv7` tag.
  {.links-list}

> A BredOS rootfs will be available soon!
> {.is-warning}

After downloading your chosen rootfs tarball, it needs to be extracted. In this example, we downloaded the Arch Linux ARM tarball and converted it to BredOS.

- Still as root extract the tarball into `/var/lib/machines/template`:

```
tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- The contents of the folder `template` should look like this:

```
ls template/
bin  boot  dev  etc  home  lib  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

- To enter the container, run:

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template
```

The parameter `--machine` defines the name of the container, while `--directory` points to the location of the container. To exit the container, use either <kbd>Ctrl</kbd> + <kbd>D</kbd> or type <kbd>Ctrl</kbd> + <kbd>]</kbd> three times within one second.

The first thing we want to do inside the container is initialize our package manager and update the system.

- To do this, run:

```
pacman-key --init
pacman-key --populate
pacman -Syu
```

> If you encounter problems resolving hostnames, remove the file `/var/lib/machines/template/etc/resolv.conf` from the host system.
> {.is-info}

- After that we need to remove some unnecessary stuff like the kernel and firmware:

```
pacman -R linux-aarch64 linux-firmware
```

- To convert the container to BredOS, run the following:

```
pacman-key --recv-keys 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
pacman-key --lsign-key 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
echo -e '# --> BredOS Mirrorlist <-- #\n\n# BredOS Main mirror\nServer = https://repo.bredos.org/repo/$repo/$arch\n' | tee /etc/pacman.d/bredos-mirrorlist
```

- Then edit the mirror file:

```
nano /etc/pacman.conf
```

- And add the following to the end of the file:

```
[BredOS-any]
Include = /etc/pacman.d/bredos-mirrorlist

[BredOS]
Include = /etc/pacman.d/bredos-mirrorlist
```

Save and close the file with <kbd>Ctrl</kbd> + <kbd>X</kbd> and <kbd>Y</kbd>

- Finally start the conversion with:

```
pacman -Syu bred-os-release BredOS-any/lsb-release bredos-logo
```

- Optionally, install bredos-config and/or bredos-news:

```
pacman -Sy bredos-config bredos-news
```

# 4. Run a container with virtual network

The container we created in section [2. Create container template](#h-3-create-container-template) used the network of your hostsystem. If you prefer a virtual network device on your container, for example if you want to use [Open vSwitch](/how-to/open-vswitch), do the following.

- If you want to do this on a new container, clone it:

```
mkdir /var/lib/machines/template-veth
rsync -avP /var/lib/machines/template/* /var/lib/machines/template-veth/
```

> To simplify this guide we will continue working with our template created in [2. Create container template](#h-3-create-container-template).
> {.is-info}

- First, enter the container like before:

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template
```

To keep the systemd theme, we use `systemd-networkd` to configure our virtual network device.

- Create two configuration files with:

```
touch /etc/systemd/network/80-container-host0.network
nano /etc/systemd/network/99-wolVeth.network
```

- Paste the following into the configuration file:

```
[Match]
Name=host0

[Network]
Address=<containers ip address> example -> 192.168.1.100/24
Gateway=<gateway of that network> example -> 192.168.1.1
DNS=<DNS Servers address> example -> 9.9.9.9
#DHCP=yes -> or comment Address, Gateway and DNS and uncomment DHCP to assign the address automatically
```

- Finally, enable `systemd-networkd`:

```
systemctl enable systemd-networkd
```

To let the container start that service, it needs to be booted (the previous command is more like chrooting). We achieve this by using the `--boot` parameter. Additionally, we add the `--network` parameter to start the container with a virtual network device.

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template --boot --network
```

This will boot the container and display the login prompt. Logging in as root is not possible, so you must either create a user before booting into the container or proceed to section [4. Run container as a service](#h-4-run-container-as-a-service).

- To create a user, run the following inside your container:

```
useradd <your username here>
passwd <your username here>
```

> As you may want to use your virtual network device for actual networking, further configuration is needed. Use, for example, [Open vSwitch](/how-to/open-vswitch) or a simple bridge device to connect the virtual network device to something.
> {.is-info}

# 🔁 4. Run a container as a service

It it possible to start a container as a service, for example to start it on boottime. There is a implementation through the systemd-nspawn@.service unit, but it requires to create override files to configure it. Our prefered way is to create a new servicefile, which contains all parameters we want to use for our container.

- Clone the template to create a new container:

```
mkdir /var/lib/machines/my-first-container
rsync -avP /var/lib/machines/template/* /var/lib/machines/my-first-container/
```

- Then create a new servicefile on your host with:

```
sudo nano /etc/systemd/system/<your containers name here>.service
```

- And paste the following into it:

```
[Unit]
Description=<your containers name here>
After=network.target
Requires=network.target

[Service]
ExecStart=/usr/bin/systemd-nspawn --machine=<your containers name here> --directory=/var/lib/machines/my-first-container --boot
KillMode=mixed
Type=notify
Restart=always

[Install]
WantedBy=multi-user.target

```

If you want to use a virtual network device on your container add, `--network` at the end of `ExecStart=/usr/...`.

- You can then start the container with:

```
sudo systemctl start <your containers name here>.service
```

- Or let it start on boottime with:

```
sudo systemctl enable <your containers name here>.service
```

- To log into your container, use `machinectl`:

```
sudo machinectl shell <your containers name here>
```

- And check all running containers (and VM's) with:

```
sudo machinectl
```

# 5. Access files/folders on host from inside a container

As the name suggests, a container typically does not have access to your host system. This can be modified to allow the container access to specific files or folders on your host system; for example, to provide additional storage space or grant the container access to your GPU.

- Access to a file/folder can be achieved with the `--bind` parameter:

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template --bind=<path to your location>
```

- For example, if you want to share your home floder:

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template --bind=/home
```

This will mount the folder `/home` to the same location within your container. If you wish to change the mount point inside your container, you can specify this by using a <kbd>:</kbd> between both paths.

- For example, if you want `/home` at `/tmp/home`:

```
systemd-nspawn --machine="Template" --directory=/var/lib/machines/template --bind=/home:/tmp/home
```

# 5. Additional Notes

`systemd-nspawn` is a extremly powerful tool. What we covered here are just the basics. Take a look at their [man page](https://www.freedesktop.org/software/systemd/man/latest/systemd-nspawn.html), if you want to be amazed!