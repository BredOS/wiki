---
title: BredOS ツール
description: BredOS が提供するユーティリティとツール
published: true
date: 2025-05-07T18:31:34.455Z
tags: null
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# BredOS ツール

`Bredos-tools` として、任意のシステムアーキテクチャと互換性があります。
BredOS の不可欠な部分。

## 入門情報

このパッケージには、開発、メンテナンス、BredOS の一般的な使用を容易にするための多くのツールが含まれています。

BredOS は好みを出荷せず、ツールと機能を出荷します。

# 🔐 GRUB パスワード保護

BredOS には、GRUBブートオプションをパスワードで制限するユーティリティが含まれています。
これにより、権限のないユーザーがデフォルト以外のエントリを起動したり、ブートパラメータを編集したりできなくなります。

## 🟢GRUBパスワードを有効にする

```
sudo grub-password
```

パスワードの入力と確認を求められます。
設定すると、デフォルトのGRUBエントリのみが認証なしで起動できます。

## 🔴 GRUBパスワードを無効にする

```
sudo grub-password -d
```

これによりパスワード制限が解除され、通常のGRUB動作が復元されます。

### メモ

設定は /etc/grub.d/99-bredos-grub-passwordに保存されます。
スクリプトはgrub-mkconfig を介して自動的に GRUB 設定を再生成します。
`/etc/grub.d/10_linux` を変更し、手動で元に戻さないでください。

# DTSCヘルパースクリプト

関数を作るには`dtc`をインストールする必要があります。`yay -S dtc`を実行してください。

スクリプトは dtc へのラッパーで、gcc 前処理、リンク、および必要なファイルの生成を自動的に実行します。
これは、デバイスツリーの生成とテストを非常に簡単になります。
基底デバイスツリーやオーバーレイを自動的に決定して生成します。

## 重要なノート

**デバイスに間違ったデバイス・ツリーをインストールすると、動作不能になります。**
**バックアップを実行し、連携プランを確認してください。**

## 使用法

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
を生成します。出力ファイル名は `-o` パラメータで設定できます。

## カーネルへのリンク

システムに複数のカーネルがインストールされている場合は、リンク先のカーネルパスを指定してください。
以下のようになります。

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

単一のカーネルがインストールされている場合、これは自動的に検出されます。

## 基本デバイスツリーのコンパイル

オーバーレイではなくベースデバイスツリーをコンパイルしている場合は、出荷されないカーネルの完全なソースが必要になります。
これは、これらのツリーには他の `.dtsi` デバイスツリーが含まれている必要があるためです。

そのような DT をコンパイルするには、 git を使用してカーネルのリポジトリを既知のパスにクローンします。

`linux-rockchip-rkr3` カーネルの例:

```
git clone https://github.com/BredOS/linux-bredos
```

次に、dtsc を実行しますが、`-i` フラグを使用して、リンクしたいファイルのフォルダを指定します。

例えば、rk3588 ボードの DT をコンパイルする場合、次のようにオプションを指定する必要があります。

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```