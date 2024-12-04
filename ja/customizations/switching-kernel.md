---
title: カーネルの切り替え
description: null
published: false
date: 2024-12-04T16:21:13.994Z
tags: null
editor: markdown
dateCreated: 2024-12-04T15:50:46.861Z
---

# 別のカーネルをインストールする

デフォルトでは、ほとんどのデバイスは `linux-rockchip-rkr3` カーネルを搭載しています。
しかし、別のカーネルから切り替えたり、別のカーネルに切り替えたりしたいかもしれません。
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

## 1. インストールされたカーネルを削除

```
sudo pacman -R linux-rockchip-rkr3 linux-rockchip-rkr3-headers
```

この時点から、リブートすることはできません。

## 2. 新しいカーネルをインストールします。

```
sudo pacman -S your-new-kernel your-new-kernel-headers
```

カーネルパッケージはinitramfsイメージを生成します。 インストールログからファイル名を確認できます:

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
