---
title: Manage containers with systemd-nspawn
description:
published: false
date: 2025-09-25T07:02:39.910Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🎛️ 1. 📥 Installing the Firmware

`systemd-nspawn` is a lightweight container tool that comes with systemd, designed to run a command or OS environment in a tightly isolated environment. Often described as "chroot on steroids," it provides a convenient way to test or run entire Linux distributions or minimal environments in a secure and controlled manner.

Unlike full virtualization solutions like QEMU or container platforms like Docker, `systemd-nspawn` uses Linux namespaces and cgroups to create containers with very little overhead.

# 3. Create container template

Containers using nspawn can be run from any location on your filesystem, but the recommended folder is `/var/lib/machines`. Inside this folder, we create a subfolder that holds our Linux/GNU rootfs. To simplify the process, this article guides you through creating a container template. The contents of that template folder can then be copied to a new location and used as a new container environment.

- Switch to root:

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

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) Look up your release of choice, then download the .tar.gz for your CPU architecture.
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) Scroll down and click on the release you want to download, then download the .tar.gz for your CPU architecture.
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) Scroll down and choose between Container Base or Container Minimal Base.
- [Arch Linux](https://archlinux.org/download/) Choose a mirror near you, then download the .tar.zst file.
- [Arch Linux ARM](https://archlinuxarm.org/os/) Download the .tar.gz file with the aarch64 or armv7 tag.
  {.links-list}

After you have downloaded your rootfs tarball of choice, we need to extract it. In this example we downloaded the Arch Linux ARM tarball and convert it to BredOS later.

- Still as root extract the tarball into `/var/lib/machines/template`:

```
sudo tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- The contents of the folder `template` should look like this:

```
ls template/
bin  boot  dev  etc  home  lib  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

