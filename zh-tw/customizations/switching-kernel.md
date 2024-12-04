---
title: Switching Kernel
description: null
published: true
date: 2024-12-04T18:04:57.653Z
tags: null
editor: markdown
dateCreated: 2024-12-04T15:50:46.861Z
---

# Installing a different kernel

By default, most devices ship with the `linux-rockchip-rkr3` kernel.
However you may wanna switch from another, or to another kernel.
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

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

From this point on it's NOT SAFE TO REBOOT.

## 2. Proceed to install the new kernel

```
sudo pacman -S your-new-kernel your-new-kernel-headers
```

The kernel package will generate an initramfs image. You can find it's filename from the install log:

```
(14/30) Updating linux initcpios...
==> Building image from preset: /etc/mkinitcpio.d/linux-rockchip-rkr3.preset: 'default'
==> Using configuration file: '/etc/mkinitcpio.conf'
  -> -k /boot/vmlinuz-linux-rockchip-rkr3 -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-rockchip-rkr3.img
==> Starting build: '6.1.75-rkr3'
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [autodetect]
  -> Running build hook: [modconf]
  -> Running build hook: [kms]
  -> Running build hook: [keyboard]
  -> Running build hook: [keymap]
  -> Running build hook: [consolefont]
==> WARNING: consolefont: no font found in configuration
  -> Running build hook: [block]
  -> Running build hook: [filesystems]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating zstd-compressed initcpio image: '/boot/initramfs-linux-rockchip-rkr3.img'
==> Initcpio image generation successful
```

The `linux-rockchip-rkr3` kernel generated the `/boot/initramfs-linux-rockchip-rkr3.img` initramfs image. Other kernels will produce different filenames.

## 3. Update bootloader config

### U-Boot

This only applies to devices that don't boot with a UEFI, if you have UEFI on your board, skip to that section.

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
```

### UEFI

This section only applies to devices that boot with UEFI. If you use U-Boot instead, skip to the above section.

Run:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 4. Reboot

Once done, you can safely reboot into the new kernel.
