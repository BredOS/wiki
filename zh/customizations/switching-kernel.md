---
title: 切换内核中
description:
published: true
date: 2025-09-13T10:25:41.121Z
tags:
editor: markdown
dateCreated: 2024-12-04T15：50：46.861Z
---

# 安装另一个内核中

默认情况下，大多数设备都使用 `linux-rockchip-rkr3` 内核。
然而，您可以从另一个开关，或者到另一个内核。
要做到这一点，请首先验证您已经安装了哪些内核：
然而，您可能想要从另一个或者切换到另一个内核。
要做到这一点，请首先验证您已经安装了哪些内核：

```
pacman -Qs linux | grep "linux"
```

这将输出一个列表，如：

```
[bill88t@duo | ~]> yay -Qs linux | grep "linux"
local/archlinux-key环20241203-1
local/archlinuxarm-key环20240419-1 (base-devel)
local/cpupower 6. 2-1 (linux-tools)
    Linux-erofs 文件系统的用户空间工具
    Linux
local/lib32-util-Linux 2.40 -1
local/linux-api-headers 6.10-1
local/linux-firmware 202411.b5885ec5-1
local/linux-firmware-whence 202411.b5885ec5-1
local/linux-rockchip-rkr3 2:6. .75-17
local/linux-rockchip-rkr3-headers 2:6.1.75-17
local/util-Linux 2.40.2-1
local/util-linux-libs 240.2-1
    util-Linux runtime 库
```

在列表中，我们可以看到linux-rockchip-rkr3和配对的头已安装。
要安装另一个内核，请先移除已安装的内核及其头部。
要安装另一个内核，请先移除已安装的内核及其头部。

## 1. 删除已安装的内核。

在上述情况下，命令是：

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

> 从这一点开始，它不会保存到REBOOT。
> {.is-danger}

## 2. 继续安装新内核。

用您选择的内核包替换<your-new-kernel>和<your-new-kernel-headers>。

```
sudo pacman -S <your-new-kernel> <your-new-kernel-headers>
```

内核包将生成一个破解图像。 您可以从安装日志中找到它的文件名： 您可以从安装日志中找到它的文件名：

```
(14/30) Updating linux initcpios...
:: Building initramfs for linux-rockchip-rkr3 (6.1.75-rkr3)
dracut[I]: Executing: /usr/bin/dracut --force --hostonly --no-hostonly-cmdline /boot/initramfs-linux-rockchip-rkr3.img 6.1.75-rkr3
dracut[I]: 74nfs: Could not find any command of 'rpcbind portmap'!
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

`linux-rockchip-rkr3`内核生成了 `/boot/initramfs-linux-rockchip-rkr3.img` drachut 图像。 其它内核会生成不同的文件名。 其它内核会生成不同的文件名。

## 3. 更新引导程序配置

> 如果你在棋盘上看到一个 BredOS 标志，你正在使用 UEFI 。
> {.is-warning}

### 3.1 U-启动

**这只适用于不使用 UEFI 启动的设备，如果您的棋盘上有UEFI，请跳至该节。**

编辑 `/boot/extlinux/extlinux.conf`:

```
sudo nano /boot/extlinux/extlinux.conf
```

它应该是这样的东西：

```
label BredOS ARM
    内核/vmlinuz-linux-rockchip-rkr3
    initrd/initramfs-linux-rockchip-rkr3.img
    fdt /dtbs/rockchip/rk3588-bluberry-edge-v10-linux. tb

    附加root=UUUID=xxxx earlycon=uart850,mmio32,0xfeb50000console=ttyFIQ0 console=tty1 consoleblank=0 loglevel=0 panic=10 root等待rw init=/sbin/init rootflags=subvol=@ rootfstype=btrfs
```

您需要编辑内核`initrd`行来指向相同的文件名(无路径)。
您还需要编辑内核行才能匹配。
要验证文件名正确，您可以列出`/boot/`的内容：
您还需要编辑内核行才能匹配。
要验证文件名正确，您可以列出`/boot/`的内容：

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

**本节仅适用于使用 UEFI 启动的设备。 如果您使用 U-Boot，请跳转到以上部分。** 如果您使用 U-Boot，请跳转到以上部分。\*\*

运行以下以重新生成 grub.cfg：

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 4. Reboot

> 完成后，您可以安全地重启到新内核。
> {.is-success}
