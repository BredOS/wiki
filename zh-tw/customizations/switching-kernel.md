---
title: Switching Kernel
description:
published: true
date: 2025-09-13T10:25:41.121Z
tags:
editor: markdown
dateCreated: 2024-12-04T15:50:46.861Z
---

# Installing a different kernel

By default, most devices ship with the `linux-rockchip-rkr3` kernel.
To do this first please validate which kernel you have installed:
To do this first please validate which kernel you have installed:

```
pacman -Qs linux | grep "linux"
```

This will output a list, like:

```
[bill88t@duo | ~]> yay -Qs linux | grep "linux"
local/archlinux-keyring 20241203-1
local/archlinuxarm-keyring 20240419-1 (base-devel)
local/cpupower 6.12-1 (linux-tools)
    Userspace utilities for linux-erofs file system
    A key remapping daemon for linux
local/lib32-util-linux 2.40.2-1
local/linux-api-headers 6.10-1
local/linux-firmware 20241111.b5885ec5-1
local/linux-firmware-whence 20241111.b5885ec5-1
local/linux-rockchip-rkr3 2:6.1.75-17
local/linux-rockchip-rkr3-headers 2:6.1.75-17
local/util-linux 2.40.2-1
local/util-linux-libs 2.40.2-1
    util-linux runtime libraries
```

In the list we can see linux-rockchip-rkr3 and the accompanying headers are installed.
To install a different kernel, first remove the installed kernel, along with it's headers.

## 1. Remove the installed kernel

With the above case the command would be:

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

> From this point on it's NOT SAFE TO REBOOT.
> {.is-danger}

## 2. Proceed to install the new kernel

Replace `<your-new-kernel>` and `<your-new-kernel-headers>` with the kernel package of your choice.

```
sudo pacman -S <your-new-kernel> <your-new-kernel-headers>
```

The kernel package will generate an initramfs image. You can find it's filename from the install log:

```
(14/30) Updating linux initcpios...
:: Building initramfs for linux-rockchip-rkr3 (6.1.75-rkr3)
dracut[I]: Executing: /usr/bin/dracut --force --hostonly --no-hostonly-cmdline /boot/initramfs-linux-rockchip-rkr3.img 6.1.75-rkr3
dracut[I]: 74nfs: Could not find any command of 'rpcbind portmap'!
dracut[I]: *** Including module: bash ***
dracut[I]: *** Including module: systemd ***
dracut[I]: *** Including module: systemd-ask-password ***
dracut[I]: *** Including module: systemd-battery-check ***
dracut[I]: *** Including module: systemd-cryptsetup ***
dracut[I]: *** Including module: systemd-initrd ***
dracut[I]: *** Including module: systemd-journald ***
dracut[I]: *** Including module: systemd-modules-load ***
dracut[I]: *** Including module: systemd-pcrphase ***
dracut[I]: *** Including module: systemd-sysctl ***
dracut[I]: *** Including module: systemd-tmpfiles ***
dracut[I]: *** Including module: systemd-udevd ***
dracut[I]: *** Including module: i18n ***
dracut[I]: *** Including module: systemd-sysusers ***
dracut[I]: *** Including module: btrfs ***
dracut[I]: *** Including module: crypt ***
dracut[I]: *** Including module: dm ***
dracut[I]: *** Including module: fs-lib ***
dracut[I]: *** Including module: kernel-modules ***
dracut[I]: *** Including module: kernel-modules-extra ***
dracut[I]: *** Including module: mdraid ***
dracut[I]: *** Including module: qemu ***
dracut[I]: *** Including module: qemu-net ***
dracut[I]: *** Including module: hwdb ***
dracut[I]: *** Including module: lunmask ***
dracut[I]: *** Including module: rootfs-block ***
dracut[I]: *** Including module: terminfo ***
dracut[I]: *** Including module: udev-rules ***
dracut[I]: *** Including module: virtiofs ***
dracut[I]: *** Including module: dracut-systemd ***
dracut[I]: *** Including module: initqueue ***
dracut[I]: *** Including module: usrmount ***
dracut[I]: *** Including module: base ***
dracut[I]: *** Including module: shell-interpreter ***
dracut[I]: *** Including module: shutdown ***
dracut[I]: *** Including module: btrfs-snapshot-overlay ***
dracut[I]: *** Including modules done ***
dracut[I]: *** Installing kernel module dependencies ***
dracut[I]: *** Installing kernel module dependencies done ***
dracut[I]: *** Resolving executable dependencies ***
dracut[I]: *** Resolving executable dependencies done ***
dracut[I]: *** Store current command line parameters ***
dracut[I]: *** Stripping files ***
dracut[I]: *** Stripping files done ***
dracut[I]: *** Creating image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' ***
dracut[I]: *** Hardlinking files ***
dracut[I]: *** Hardlinking files done ***
dracut[I]: Using auto-determined compression method 'zstd'
dracut[I]: *** Creating initramfs image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' done ***
dracut[I]: *** Moving image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' to '/boot/initramfs-linux-rockchip-rkr3.img' ***
dracut[I]: *** Moving image file '/boot/initramfs-linux-rockchip-rkr3.img.tmp' to '/boot/initramfs-linux-rockchip-rkr3.img' done ***
```

The `linux-rockchip-rkr3` kernel generated the `/boot/initramfs-linux-rockchip-rkr3.img` initramfs image. Other kernels will produce different filenames.

## 3. Update bootloader config

> If during board power-on you see a BredOS logo, you are using UEFI.
> {.is-warning}

### 3.1 U-Boot

**This only applies to devices that don't boot with a UEFI, if you have UEFI on your board, skip to that section.**

Edit `/boot/extlinux/extlinux.conf`:

```
sudo nano /boot/extlinux/extlinux.conf
```

Inside it it should be something like this:

```
label BredOS ARM
    kernel /vmlinuz-linux-rockchip-rkr3
    initrd /initramfs-linux-rockchip-rkr3.img
    fdt /dtbs/rockchip/rk3588-blueberry-edge-v10-linux.dtb

    append root=UUID=xxxx earlycon=uart8250,mmio32,0xfeb50000 console=ttyFIQ0 console=tty1 consoleblank=0 loglevel=0 panic=10 rootwait rw init=/sbin/init rootflags=subvol=@ rootfstype=btrfs
```

You need to edit the kernel `initrd` line to point to the same filename (without the path).
You also need to edit the kernel line to match that.
To verify the filename is correct, you can list the contents of `/boot/`:

```
ls /boot/
dtbs  
efi  
extlinux  
grub  
initramfs-linux-rockchip-rkr3.img  
vmlinuz-linux-rockchip-rkr3
```

### 3.2 UEFI

**This section only applies to devices that boot with UEFI. If you use U-Boot instead, skip to the above section.**

Run the following to regenerate the grub.cfg:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 4. Reboot

> Once done, you can safely reboot into the new kernel.
> {.is-success}
