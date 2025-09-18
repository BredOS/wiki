---
title: Mri GPUでRK3588をセットアップする
description:
published: true
date: 2025-09-18T07:07:37.654Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# 1. はじめに

このガイドでは、RK3588チップセットを搭載したボードに搭載されているMali GPUでPanthorを有効にするための手順を説明します。

# 2. Panthor DTBO を有効にする

## 自動的に2.1

- bredos-config ツールは、dtbo を有効/無効にする簡単な方法を提供します。 ツールを起動する ツールを以下から起動します。

```
sudo bredos-config
```

次に、`Device Tree Manager` -> `Enable / Disable Overlays` に移動し、`rockchip-rk3588-panthor-gpu` を有効にします。 次に、ツールはベースデバイスツリーと選択したオーバーレイをインストールします。

> 画面の指示に従ってください!
> {.is-warning}

bredos-config は dtbs をインストールして grub 設定を変更することができますが、起動時にそれらをロードするには _uefi 設定を変更できません_ 。 これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。 The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos). これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。 The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos).

> dtb オーバーレイのインストール後、システムを再起動しないでください!
> \`3で続行します。 Panfork グラフィックスを置き換えます。
> {.is-warning}

## 2.2 手動で

[Device Tree Overlay guide](/how-to/how-to-enable-dtbos)に従って、
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**DTBOをコピーした後、システムを再起動しないでください！**

> dtb オーバーレイのインストール後、システムを再起動しないでください!
> \`3で続行します。 Panfork グラフィックスを置き換えます。
> {.is-warning}

# 3. Panfork グラフィックスを置き換え

- `mesa-panfork-git` パッケージを標準の `mesa` パッケージに置き換えます。

```
sudo pacman -S mesa
```

# 4. システムを再起動

- vulkanローダーとドライバーをインストールします:

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

# 5. システムを再起動

- システムを再起動して変更を適用します。 グラフィックを検証したい場合は、以下を実行できます。

```
sudo pacman -S inxi mesa-utils
inxi -G
```