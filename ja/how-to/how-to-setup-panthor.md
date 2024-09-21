---
title: 🐾 マリGPUでRK3588を使ってパンターをセットアップする方法
description: null
published: true
date: 2024-09-01T16:18:22.222Z
tags: null
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# RK3588 🚀 でマリGPUでPanthorを有効にする

このガイドでは、RK3588チップセットを搭載したボードに搭載されているMali GPUでPanthorを有効にするための手順を説明します。

# 🔧 パンターを有効にする手順

## UEFI対応デバイス

### 🖥️ 1. UEFIの初期セットアップ

まず、DTB ファイルに必要なディレクトリを作成します。

```
sudo mkdir -p /boot/dtb/{base,overlays}
```

次に、UEFI設定を設定します。 UEFI > Device Manager > Rockchip プラットフォーム設定 > ACPI / Device Treeを起動し、以下の操作を行います:

- **設定テーブルモードを`デバイスツリー`に設定**
- **`Support DTB overlays` を `Enabled`** に変更します

![](/panthor/enable_tree_dtb_in_uefi.jpg)

F10を押してシステムに保存して起動します(最初のUEFI画面に戻り、「続ける」を選択することができます)。

### 🛠️ 3. デバイス ツリーのセットアップ

> FydeTab Duo を使っている場合は、特定の DTB ファイルを `base` フォルダにコピーします。
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb /boot/dtb/base/
> sudo cp /boot/dtb/base/rk3588s-fydetab-duo.dtb /boot/dtb/base/rk3588s-table-12c-linux.dtb
> ```

{.is-info}

他のRK3588ベースのボードについては、実際のデバイス名に`rk3588-board.dtb`を置き換えてください:

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb /boot/dtb/base/
```

### 🌐 4. すべてのボードの一般的なセットアップ

使用しているボードに関係なく、DTBOオーバーレイファイルをコピーしてPanthorを有効にします。

```
sudo cp /boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo /boot/dtb/overlays/
```

さらに、GRUBの設定を変更する必要があります。

GRUB設定ファイルを開く

```
sudo nano /etc/default/grub
```

`#`を最初に追加して、次の行にコメントします。

```
# GRUB_DTB="dtbs/rockchip/rk3588s-fydetab-duo.dtb"
```

新しい設定でGRUBを更新

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🔄 5. mesa-panfork-git を置き換え

`mesa-panfork-git` パッケージを標準の `mesa` パッケージに置き換えます。

```
sudo pacman -S mesa
```

### 🔁 6. システムを再起動

## ⚙️ U-Boot 対応デバイス

### 1. Panthor DTBO を有効にする

オーバーレイを適用するために、 `extlinux` 設定ファイルを編集します。

```
sudo nano /boot/extlinux/extlinux.conf
```

`extlinux.conf`ファイルに次の行を追加します。

```
fdtoverlays /dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo
```

### 🔄 2. mesa-panfork-git を置き換え

`mesa-panfork-git` パッケージを標準の `mesa` パッケージに置き換えます。

```
sudo pacman -S mesa
```

### 🔁 3. システムを再起動
