---
title: 📟 DTBOs を有効にする方法
description: null
published: true
date: 2025-05-15T13:00:37.165Z
tags: null
editor: markdown
dateCreated: 2024-11-10T18:02:07.427Z
---

# デバイスツリーオーバーレイを有効にする方法

**はじめに**
異なるデバイスツリーオーバーレイ(DTBOs)を有効にすると、Linuxカーネルを再コンパイルせずにオプションのハードウェアまたはカーネルの変更を有効にできます。
これは、パンターグラフィックスタックを有効にするための方法でもあります。

---

# 💻 UEFI搭載システム用

UEFI搭載ボードで実行している場合は、設定する必要があります。
前にすでにこれを行っている場合は、手順5に進むことができます。

> 2024年9月12日以降の画像は`/boot`の代わりに`/boot/efi`を使用します。
> {.is-info}

To determine where your ESP partition is located, run the command,
`df | grep "/boot" | awk '{print $NF}'` and **replace **`<ESP>`** IN ALL OF THE FOLLOWING commands** with it's output.

### 📁 1: DTBファイルを保存するために必要なディレクトリを作成します。

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

### :file_cabiet: 2: DTBをベースにコピーする

> FydeTab Duo を使っている場合は、特定の DTB ファイルを `base` フォルダにコピーします。
>
> ```
> sudo cp /boot/dtbs/rockchip/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/
> sudo cp <ESP>/dtb/base/rk3588s-fydetab-duo.dtb <ESP>/dtb/base/rk3588s-table-12c-linux.dtb
> ```

{.is-info}

他のRK3588ベースのボードについては、実際のデバイス名に`rk3588-board.dtb`を置き換えてください:

```
sudo cp /boot/dtbs/rockchip/rk3588-board.dtb <ESP>/dtb/base/
```

### 🫘 3: GRUB の設定

GRUB設定ファイルを開きます:

```
sudo nano /etc/default/grub
```

`#`を最初に追加して、次の行にコメントします。

```
# GRUB_DTB="dtbs/rockchip/device tree.dtb"
```

\*(DTBはそこで異なります) \*

新しい設定でGRUBを更新:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 🎛️ 4: UEFI の設定

UEFI _（GRUBからこれを行うことができます）_ > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`を再起動し、以下の操作を行います：

- **設定テーブルモードを`デバイスツリー`に設定**
- **`Support DTB overlays` を `Enabled`** に変更します

![](/panthor/enable_tree_dtb_in_uefi.jpg)

F10を押して保存し、システムに再起動します(最初のUEFI画面に戻り、`Continue`を選択することができます)。

### 🔄 5: DTBO をコピー

`my-overlay`をお好みのdtboに置き換えてください。

```
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

### <unk> 6: 再起動

変更を適用するには、システムを再起動します。

# ⚙️ U-Boot 搭載デバイスで

### 1. extlinux 設定を編集

extlinuxの設定は以下を実行することで編集できます。

```
sudo nano /boot/extlinux/extlinux.conf
```

ファイルの一番下に次の行を追加し、DTBO を選択したものに置き換えます。

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```

### 重要なノート

\*\*`/boot` や `<ESP>` をこれらの行に追加しないでください。

**fdtoverlays**行を1つ以上追加しないでください。
複数のDTBOを有効にしたい場合は、空白文字で区切られた1行に追加します。
例:

```
fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
```