---
title: デバイスツリー
description:
published: true
date: 2025-05-15T12:51:43.781Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# デバイスツリー

デバイス ツリーは、ARM および RISC-V システムで一般的に使用されるハードウェアを記述するためのメカニズムです。 カーネルドライバのコードを変更せずに、カーネルがハードウェアデバイスを検出して設定できるようにします。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。

## UEFIおよびGrab システムでのデバイスツリーの切り替え

grub 設定ファイル `/etc/default/grub` を開きます。
grub 設定ファイル `/etc/default/grub` を開きます。
`GRUB_DTB=`で始まる行を探し、デバイスのツリーファイルへのパスを追加します。例:

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```

次に、grub の設定を更新します。

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

**注意:** DTBを指定できるのは1つだけです。

## Updating Device Trees in U-Boot systems with extlinux

Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`, find the line with `fdt`, for example:

```bash
fdt /dtbs/rockchip/xxx.dtb
```

Then reboot.

**注意:** DTBを指定できるのは1つだけです。