---
title: Run Virtual Machines on BredOS
description: 
published: true
date: 2025-09-17T10:43:46.119Z
tags: vm, how-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 1. Introduction

This guide will help you set up and manage virtual machines using `virt-manager` on BredOS.

# 2. Prerequisites

Before you begin, ensure that you have the following:

- A working internet connection
- `sudo` privileges

# 3. Installation
## 3.1 Install Required Packages

- To start, you need to install the necessary packages for `qemu` and `virt-manager`.

```
sudo pacman -Syu virt-manager virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```
> While `qemu` is your hypervisor, `virt-manager` is a GUI-based tool for managing it.
{.is-info}

## 3.2 Enable and Start the Libvirt Service

- Once the packages are installed, enable and start the `libvirtd` service:

```bash
sudo systemctl enable --now libvirtd
```

- To verify that the service is running:

```bash
sudo systemctl status libvirtd
```

## 3.3 Add Your User to the `libvirt` Group

- To avoid needing root privileges for managing VMs, add your user to the `libvirt` group:

```bash
sudo usermod -aG libvirt $(whoami)
```
> This does allow managing VMs from user-level. This can be dangerous!
{.is-warning}

- After adding yourself to the group, log out and log back in for the changes to take effect.

## 3.4 Configure Networking

- `virt-manager` uses `dnsmasq` for network management. You may want to ensure `libvirt` is set up with default network settings:

```bash
sudo virsh net-start default
sudo virsh net-autostart default
```

## 3.5 Launch Virt-Manager

- Now that everything is set up, you can start `virt-manager`:

```bash
virt-manager
```

- This will open the `virt-manager` GUI where you can create and manage virtual machines.

![virt.jpg](/vms/virt.jpg)
> If you have not added your user to the group `libvirt` you need to enter your password now.
{.is-info}

## 3.6 Enable XML editing
- To enable XML editing (needed later) you need to open `virt-manager`, then navigate to `Edit` then `Preferences` and `Enable XML editing`.

# 4. Create a Virtual Machine
- Inside `virt-manager` click on the display icon or navigate to `File` -> `Create virtual machine` to create a new virtual machine.

- Select the installation source (Local install media or Network Install).

- If you choose local installation media, use the wizard to select your .iso file.

- Follow the wizard to allocate CPU, RAM, and storage for your VM.

> On the RK3588 you can allocate max 4 cores per vm due to the little big architecture.
{.is-warning}

- Before you click `Finish` you need to check "**Customize configuration before install**" and edit the xml responsible for allocating cpu cores.

- Click `Finish`

A new window opens, allowing you to edit the settings of your virtual machine before creating it.- Open the CPUs configuration and then the XML tab

- Locate `<vcpu>XYZ</vcpu>` and replace it with 
```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```
> Where `cpu set` is the cores you want to use 0-3 are the E cores on the rk3588 and 4-7 are the performance cores and the number of cores. In the example above the vm will have 2 cores with them being efficiency cores aka cores 1 and 2 on the die itself.
{.is-info}

- Once configured, start the VM.

> There we have it. Now you can run Bred inside Bred! 
{.is-success}


# 5. Additional Configuration

- To manage VMs via command line, you can use `virsh`:

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

# 6. Troubleshooting

- **Permission Issues**: Ensure your user is in the `libvirt` group and that the `libvirtd` service is running.
- **Networking Issues**: If VMs don't have internet access, ensure the default `virsh` network is running.

