---
title: デバイスツリー
description:
published: true
date: 2025-05-15T12:51:43.781Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# 1. はじめに

デバイス ツリーは、ARM および RISC-V システムで一般的に使用されるハードウェアを記述するためのメカニズムです。 カーネルドライバのコードを変更せずに、カーネルがハードウェアデバイスを検出して設定できるようにします。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。
デバイス ツリーは、ARM および RISC-V システムで一般的に使用されるハードウェアを記述するためのメカニズムです。 カーネルドライバのコードを変更せずに、カーネルがハードウェアデバイスを検出して設定できるようにします。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。
デバイス ツリーは、ARM および RISC-V システムで一般的に使用されるハードウェアを記述するためのメカニズムです。 カーネルドライバのコードを変更せずに、カーネルがハードウェアデバイスを検出して設定できるようにします。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。
ACPIテーブルがハードウェアの自動検出と構成を可能にするx86システムとは異なります。 ほとんどのARMシステムでは、ハードウェアの変更を宣言するためにデバイスツリーを変更する必要があります。

# 2. デバイスツリー

## UEFIおよびGrab システムでのデバイスツリーの切り替え

Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`, find the line with `fdt`, for example:

- grub 設定ファイル `/etc/default/grub` を開きます。
  `GRUB_DTB=`で始まる行を探し、デバイスのツリーファイルへのパスを追加します。例:

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```

- 次に、grub の設定を更新します。

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

> DTBは1つしか指定できません。
> {.is-info}
> {.is-info}
> {.is-info}

## Updating Device Trees in U-Boot systems with extlinux

- Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`, find the line with `fdt`, for example: 例えば、`fdt`の行を見つけます。

```bash
fdt /dtbs/rockchip/xxx.dtb
```

次に、デバイス ツリー パスに合わせて編集します。 保存してシステムを再起動します。 保存してシステムを再起動します。 保存してシステムを再起動します。

> DTBは1つしか指定できません。
> {.is-info}
> {.is-info}
> {.is-info}
