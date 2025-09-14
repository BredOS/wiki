---
title: 🐾 マリGPUでRK3588を使ってパンターをセットアップする方法
description:
published: true
date: 2025-09-13T09:17:09.327Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# RK3588 🚀 でマリGPUでPanthorを有効にする

このガイドでは、RK3588チップセットを搭載したボードに搭載されているMali GPUでPanthorを有効にするための手順を説明します。

## 🎛️ 1. Panthor DTBO を有効にする

### 🤖 1.1 自動

bredos-config ツールは、dtbo を有効/無効にする簡単な方法を提供します。 ツールを起動する ツールを起動する

```
sudo bredos-config
```

を選択し、`Device Tree Manager` -> `Enable / Disable Overlays` に移動し、`rockchip-rk3588-panthor-gpu` を有効にします。 次に、ツールはベースデバイスツリーと選択したオーバーレイをインストールします。 次に、ツールはベースデバイスツリーと選択したオーバーレイをインストールします。

> 画面の指示に従ってください!
> {.is-warning}

bredos-config は dtbs をインストールして grub 設定を変更することができますが、起動時にそれらをロードするには _uefi 設定を変更できません_ 。 これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。 The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos). これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。 The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos).

### 🦶 1.2 手動で

[Device Tree Overlay guide](/how-to/how-to-enable-dtbos)に従って、
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**DTBOをコピーした後、システムを再起動しないでください！**

> dtb オーバーレイのインストール後、システムを再起動しないでください!
> {.is-warning}

## 🔄 2. Panfork グラフィックスを置き換え

`mesa-panfork-git` パッケージを標準の `mesa` パッケージに置き換えます。

```
sudo pacman -S mesa
```

## 🔁 3. システムを再起動

vulkanローダーとドライバーをインストールします:

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

## 🔁 4. システムを再起動

システムを再起動して変更を適用します。 グラフィックを検証したい場合は、以下を実行できます。

```
sudo pacman -S inxi mesa-utils
inxi -G
```