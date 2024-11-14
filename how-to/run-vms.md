---
title: How to run Virtual Machines on BredOS
description: 
published: true
date: 2024-11-14T19:23:33.286Z
tags: vm, how-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 🚀 Running Virtual Machines with Virt-Manager on BredOS

This guide will help you set up and manage virtual machines using `virt-manager` on BredOS.

## 📋 Prerequisites

Before you begin, ensure that you have the following:

- A working internet connection 🌐
- Sudo privileges 🔑

## Step 1: Install Required Packages 📦

To start, you need to install the necessary packages for KVM and `virt-manager`.

```bash
sudo pacman -Syu
sudo pacman -S virt-manager virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

## Step 2: Enable and Start the Libvirt Service 🖧

Once the packages are installed, enable and start the `libvirtd` service:

```bash
sudo systemctl enable --now libvirtd
```

To verify that the service is running:

```bash
sudo systemctl status libvirtd
```

## Step 3: Add Your User to the `libvirt` Group 👥

To avoid needing root privileges for managing VMs, add your user to the `libvirt` group:

```bash
sudo usermod -aG libvirt $(whoami)
```

After adding yourself to the group, log out and log back in for the changes to take effect.

## Step 4: Configure Networking 🌐

`virt-manager` uses `dnsmasq` for network management. You may want to ensure `libvirt` is set up with default network settings:

```bash
sudo virsh net-start default
sudo virsh net-autostart default
```

## Step 5: Launch Virt-Manager 🖥️

Now that everything is set up, you can start `virt-manager`:

```bash
virt-manager
```

This will open the `virt-manager` GUI where you can create and manage virtual machines.
![virt.jpg](/vms/virt.jpg)
## Step 6: Enable XML editing
To enable XML editing (Needed later) you need to open `virt-manager` go to **Edit** then **Preferences** and enable XML editing 
![xmlediting.jpg](/vms/xmlediting.jpg)
## Step 7: Create a Virtual Machine 🛠️

1. Open `virt-manager`.
![virt.jpg](/vms/virt.jpg)
2. Click on **Create a new virtual machine** ➕.
![virtnewvm.jpg](/vms/virtnewvm.jpg)
3. Select the installation source (ISO image or network install).
![newvm.jpg](/vms/newvm.jpg)
4. Follow the wizard to allocate CPU, RAM, and storage for your VM. ⚙️
> On the RK3588 you can allocate max 4 cores per vm due to the little big architecture
{.is-warning}

![disk.jpg](/vms/disk.jpg)
![cpuram.jpg](/vms/cpuram.jpg)
5. On CPUs with the little.big architecture like the RK3588 you need to check "Customize configuration before install" and edit the xml responsible for allocating cpu cores
![finalstep.jpg](/vms/finalstep.jpg)
Click **Finish**
![vcpuxml0.jpg](/vms/vcpuxml0.jpg)
Open the **CPUs** configuration and then the **XML** tab
![vcpuxml1.jpg](/vms/vcpuxml1.jpg)
Locate `<vcpu>XYZ</vcpu>` and replace it with 
```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```
Where cpu set is the cores you want to use 0-3 are the E cores on the rk3588 and 4-7 are the performance cores and the number of cores. In the example above the vm will have 2 cores with them being efficiency cores aka cores 1 and 2 on the die itself.
![vcpuxml2.jpg](/vms/vcpuxml2.jpg)

5. Once configured, start the VM. 🟢

![startvm.jpg](/vms/startvm.jpg)

## Additional Configuration ⚙️

- To manage VMs via command line, you can use `virsh`:

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

## Troubleshooting 🛠️

- **Permission Issues**: Ensure your user is in the `libvirt` group and that the `libvirtd` service is running.
- **Networking Issues**: If VMs don't have internet access, ensure the default `virsh` network is running.

## 🎉 Conclusion

You have successfully set up `virt-manager` on BredOS and are ready to create and manage virtual machines!
