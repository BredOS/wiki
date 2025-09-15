---
title: DTBOを有効にする方法
description:
published: true
date: 2025-09-15T08:30:36.658Z
tags:
editor: markdown
dateCreated: 2024-11-10T18:02:07.427Z
---

# 1. はじめに

異なるデバイスツリーオーバーレイ(DTBO)を有効にすると、Linuxカーネルを再コンパイルせずにオプションのハードウェアまたはカーネルの変更を有効にできます。

> これはカーネルの動作を変更するための方法でもあります。 例えば、パンターグラフィックススタックを有効にしたり、システムのLEDを無効にしたりします。
> {.is-success}

# 2. BredOS-Config

bredos-config ツールは、dtbo を有効/無効にする簡単な方法を提供します。 ツールを起動する ツールを起動する

```
sudo bredos-config
```

を選択し、`Device Tree Manager` -> `Enable / Disable Overlays` に移動し、dtb overlaysを好みに合わせて有効にします。 次に、ツールはベースデバイスツリーと選択したオーバーレイをインストールします。

> 注意深く画面の指示に従うか、3.4 UEFIを設定してください!
> {.is-warning}

bredos-config は dtbs をインストールして grub 設定を変更することができますが、起動時にそれらをロードするには _uefi 設定を変更できません_ 。 これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。 The changes can also be found in the [Device Tree Overlay guide](/how-to/how-to-enable-dtbos). これはユーザーが行う必要があります。 ユーザーが行わなければならない変更は、base/overlay dtbsの最初のインストール時にbredos-configによって表示されます。

# 3. UEFI搭載システム用

UEFI搭載ボードで実行している場合は、設定する必要があります。
前にすでにこれを行っている場合は、手順5に進むことができます。
前にすでにこれを行っている場合は、手順5に進むことができます。

> 2024年9月12日以降の画像は`/boot`の代わりに`/boot/efi`を使用します。
> {.is-info}
> {.is-info}

To determine where your ESP partition is located, run the command,
`df | grep "/boot" | awk '{print $NF}'` and **replace **`<ESP>`** IN ALL OF THE FOLLOWING commands** with it's output.

## 3.1 DTB ファイルを保存するために必要なディレクトリを作成します。

```
sudo mkdir -p <ESP>/dtb/{base,overlays}
```

## 3.2 ベース DTB 上にコピー

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

## 3.3 GRUB の設定

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

## 3.4 UEFI の設定

UEFI _（GRUBからこれを行うことができます）_ > `Device Manager` > `Rockchip Platform Configuration` > `ACPI / Device Tree`を再起動し、以下の操作を行います：

- **設定テーブルモードを`デバイスツリー`に設定**
- **`Support DTB overlays` を `Enabled`** に変更します

![](/panthor/enable_tree_dtb_in_uefi.jpg)

F10を押して保存し、システムに再起動します(最初のUEFI画面に戻り、`Continue`を選択することができます)。

## 3.5 DTBO をコピー

`my-overlay`をお好みのdtboに置き換えてください。

```
sudo cp /boot/dtbs/rockchip/overlay/my-overlay.dtbo <ESP>/dtb/overlays/
```

## 3.6 Reboot

変更を適用するには、システムを再起動します。

# 4. U-Boot Powered デバイスで

## 4.1 extlinux 設定を編集

extlinuxの設定は以下を実行することで編集できます。

```
sudo nano /boot/extlinux/extlinux.conf
```

ファイルの一番下に次の行を追加し、DTBO を選択したものに置き換えます。

```
fdtoverlays /dtbs/rockchip/overlay/my-overlay.dtbo
```

> **fdtoverlays**行を1つ以上追加しないでください。
> **fdtoverlays**行を1つ以上追加しないでください。
> 複数のDTBOを有効にしたい場合は、空白文字で区切られた1行に追加します。
> 例:
> 例:
> **fdtoverlays**行を1つ以上追加しないでください。
> 複数のDTBOを有効にしたい場合は、空白文字で区切られた1行に追加します。
> 例:
> 例:
>
> ```
> fdtoverlays /dtbs/rockchip/overlay/overlay1.dtbo /dtbs/rockchip/overlay/overlay2.dtbo
> ```

{.is-warning}
