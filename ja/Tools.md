---
title: BredOS ツール
description: BredOS が提供するユーティリティとツール
published: true
date: 2025-05-07T18:31:34.455Z
tags:
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# 1. 入門情報

これは `bredos-tools` として出荷されており、任意のシステムアーキテクチャと互換性があります。
それはBredOSの不可欠な部分です。 `bredos-tools` はデフォルトでインストールする必要があります。
それはBredOSの不可欠な部分です。 `bredos-tools` はデフォルトでインストールする必要があります。

- インストールしていない場合:

```
sudo pacman -S bredos-tools
```

このパッケージには、開発、メンテナンス、BredOS の一般的な使用を容易にするための多くのツールが含まれています。

# 2. 🔐 GRUB パスワード保護

BredOS には、GRUBブートオプションをパスワードで制限するユーティリティが含まれています。
これにより、権限のないユーザーがデフォルト以外のエントリを起動したり、ブートパラメータを編集したりできなくなります。
これにより、権限のないユーザーがデフォルト以外のエントリを起動したり、ブートパラメータを編集したりできなくなります。
これにより、権限のないユーザーがデフォルト以外のエントリを起動したり、ブートパラメータを編集したりできなくなります。

## 🟢GRUBパスワードを有効にする

- grub パスワード保護を有効にするには、次を実行します。

```
sudo grub-password
```

パスワードの入力と確認を求められます。
パスワードの入力と確認を求められます。
パスワードの入力と確認を求められます。
設定すると、デフォルトのGRUBエントリのみが認証なしで起動できます。

## 🔴 GRUBパスワードを無効にする

- grub パスワード保護を無効にするには、次を実行します。

```
sudo grub-password -d
```

これによりパスワード制限が解除され、通常のGRUB動作が復元されます。

> 設定は /etc/grub.d/99-bredos-grub-passwordに保存されます。
> スクリプトはgrub-mkconfig を介して自動的に GRUB 設定を再生成します。
> 設定は /etc/grub.d/99-bredos-grub-passwordに保存されます。
> スクリプトはgrub-mkconfig を介して自動的に GRUB 設定を再生成します。
> `/etc/grub.d/10_linux` を変更し、手動で元に戻さないでください。
> スクリプトはgrub-mkconfig を介して自動的に GRUB 設定を再生成します。
> これは `/etc/grub.d/10_linux` を変更し、手動で元に戻さないでください。
> {.is-info}

# 3. DTSCヘルパースクリプト

- 関数を作るには`dtc`をインストールする必要があります。`yay -S dtc`を実行してください。

```
yay -S dtc
```

スクリプトは dtc へのラッパーで、gcc 前処理、リンク、および必要なファイルの生成を自動的に実行します。
これは、デバイスツリーの生成とテストを非常に簡単になります。
基底デバイスツリーやオーバーレイを自動的に決定して生成します。
これは、デバイスツリーの生成とテストを非常に簡単になります。
それに応じて基底デバイスツリーやオーバーレイを自動的に決定して生成します。

> デバイスに不正なデバイス ツリーをインストールすると、動作しなくなります。
> 注意してバックアップを実行し、連帯プランを確認してください。
> {.is-warning}
> 注意してバックアップを実行し、連帯プランを確認してください。
> {.is-warning}

## 3.1 使用法

- パラメータ`-h`を指定してdtscを実行すると、以下のようになります。

```
usage: dtsc [-h] [-o OUTPUT] [-i INCLUDE] [-k KERNEL] [input]

Compile a Device Tree Source (DTS) file into a Device Tree Blob (DTBO or DTB).

positional arguments:
  input                 Input DTS file

options:
  -h, --help            show this help message and exit
  -o, --output OUTPUT   Output file (default: makes input_filename.dtb)
  -i, --include INCLUDE
                        Source of additional device tree files (optional)
  -k, --kernel KERNEL   Manualy specify a kernel source path (default:
                        autodetect)

Example: ./compile_dts.py my_device_tree.dts -o output.dtbo
```

## Input

スクリプトは入力 `.dts` ファイルを期待します。 出力が指定されていない場合は、一致する名前 `.dtb`
を生成します。出力ファイル名は `-o` パラメータで設定できます。 出力が指定されていない場合は、一致する名前 `.dtb`
を生成します。出力ファイル名は `-o` パラメータで設定できます。 出力が指定されていない場合は、一致する名前 `.dtb`
を生成します。出力ファイル名は `-o` パラメータで設定できます。

## 3.3 カーネルとのリンク

システムに複数のカーネルがインストールされている場合は、リンク先のカーネルパスを指定してください。
以下のようになります。
以下のようになります。

- 以下のようになります。

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

単一のカーネルがインストールされている場合、これは自動的に検出されます。

## 基本デバイスツリーのコンパイル

オーバーレイではなくベースデバイスツリーをコンパイルしている場合は、出荷されないカーネルの完全なソースが必要になります。
これは、これらのツリーには他の `.dtsi` デバイスツリーが含まれている必要があるためです。
これは、これらのツリーには他の `.dtsi` デバイスツリーが含まれている必要があるためです。
これは、これらのツリーには他の `.dtsi` デバイスツリーが含まれている必要があるためです。

そのような DT をコンパイルするには、 git を使用してカーネルのリポジトリを既知のパスにクローンします。

- `linux-rockchip-rkr3` カーネルの例:

```
git clone https://github.com/BredOS/linux-bredos
```

次に、dtsc を実行しますが、`-i` フラグを使用して、リンクしたいファイルのフォルダを指定します。

- 例えば、rk3588 ボードの DT をコンパイルする場合、次のようにオプションを指定する必要があります。

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```