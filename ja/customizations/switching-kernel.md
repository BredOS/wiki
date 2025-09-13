---
title: カーネルの切り替え
description:
published: true
date: 2025-09-13T10:25:41.121Z
tags:
editor: markdown
dateCreated: 2024-12-04T15:50:46.861Z
---

# 別のカーネルをインストールする

デフォルトでは、ほとんどのデバイスは `linux-rockchip-rkr3` カーネルを搭載しています。
しかし、別のカーネルから切り替えたり、別のカーネルに切り替えたりしたいかもしれません。
これを行うには、最初にインストールしたカーネルを確認してください:
ただし、別のカーネルやカーネルに切り替えたい場合があります。
これを行うには、最初にインストールしたカーネルを確認してください:

```
pacman -Qs linux | grep "linux"
```

次のようにリストを出力します。

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

リストにはlinux-rockchip-rkr3とそれに付随するヘッダーがインストールされています。
別のカーネルをインストールするには、最初にインストールされたカーネルとそのヘッダを削除します。
別のカーネルをインストールするには、最初にインストールされたカーネルとそのヘッダを削除します。

## 1. インストールされたカーネルを削除

上記の場合、コマンドは次のようになります:

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

> この時点から、リブートすることはできません。
> {.is-danger}

## 2. 新しいカーネルをインストールします。

選択したカーネルパッケージに`<your-new-kernel>`と`<your-new-kernel-headers>`を置き換えます。

```
sudo pacman -S <your-new-kernel> <your-new-kernel-headers>
```

カーネルパッケージはinitramfsイメージを生成します。 インストールログからファイル名を確認できます: インストールログからファイル名を確認できます:

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

`linux-rockchip-rkr3` カーネルは `/boot/initramfs-linux-rockchip-rkr3.img` initramfs イメージを生成します。 他のカーネルは異なるファイル名を生成します。 他のカーネルは異なるファイル名を生成します。

## 3. ブートローダーの設定を更新する

> ボードの電源投入中にBredOSのロゴが表示される場合は、UEFIを使用しています。
> {.is-warning}

### 3.1 U-Boot

**これは、UEFIがボードにある場合は、UEFIで起動しないデバイスにのみ適用されます。そのセクションにスキップしてください。**

`/boot/extlinux/extlinux.conf`を編集:

```
sudo nano /boot/extlinux/extlinux.conf
```

その中には以下のようなものがあります:

```
label BredOS ARM
    kernel /vmlinuz-linux-rockchip-rkr3
    initrd /initramfs-linux-rockchip-rkr3.img
    fdt /dtbs/rockchip/rk3588-blueberry-edge-v10-linux.dtb

    append root=UUID=xxxx earlycon=uart8250,mmio32,0xfeb50000 console=ttyFIQ0 console=tty1 consoleblank=0 loglevel=0 panic=10 rootwait rw init=/sbin/init rootflags=subvol=@ rootfstype=btrfs
```

カーネル`initrd`行を編集して同じファイル名を指すようにする必要があります (パスなし)。
それに合わせてカーネル行を編集する必要があります。
ファイル名が正しいことを確認するには、`/boot/`の内容をリストすることができます。
それに合わせてカーネル行を編集する必要があります。
ファイル名が正しいことを確認するには、`/boot/`の内容をリストすることができます。

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

**このセクションはUEFIで起動するデバイスにのみ適用されます。 代わりに U-Boot を使用する場合は、上記のセクションにスキップしてください。**

grub.cfg を再生成するには、以下を実行します。

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 4. Reboot

> 完了したら、安全に新しいカーネルに再起動できます。
> {.is-success}
