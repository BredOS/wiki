---
title: DTSC Helper Script
description: BredOS デバイスツリーソースコンパイラヘルパースクリプトの使用
published: true
date: 2025-05-07T13:40:24.351Z
tags: null
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# DTSC Helper Script

`dtsc` は、 `bredos-tools` パッケージと共にBredOS と共にデフォルトで出荷されるコマンドです。
しかし、`dtc`をインストールするには、 `yay -S dtc`を実行してください。

スクリプトは、dtscのラッパーであり、gcc の自動前処理、リンク、および必要なファイルの生成を行います。
これは、デバイスツリーの生成とテストを非常に簡単になります。
基底デバイスツリーやオーバーレイを自動的に決定して生成します。

## 重要なノート

**デバイスに間違ったデバイス・ツリーをインストールすると、動作不能になります。**
**バックアップを実行し、連携プランを確認してください。**

# 使用法

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

The script expects an input `.dts` file. 出力が指定されていない場合は、一致する名前 `.dtb`
を生成します。出力ファイル名は `-o` パラメータで設定できます。

## Linking against kernel

システムに複数のカーネルがインストールされている場合は、リンク先のカーネルパスを指定してください。
以下のようになります。

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

単一のカーネルがインストールされている場合、これは自動的に検出されます。

## 基本デバイスツリーのコンパイル

If you're compiling a base device tree and not an overlay, you'll need your kernel's full sources, which are not shipped.
これは、これらのツリーには他の `.dtsi` デバイスツリーが含まれている必要があるためです。

To compile such a DT, clone your kernel's repository using git, onto a known path.

`linux-rockchip-rkr3` カーネルの例:

```
git clone https://github.com/BredOS/linux-bredos
```

次に、dtsc を実行しますが、`-i` フラグを使用して、リンクしたいファイルのフォルダを指定します。

例えば、rk3588 ボードの DT をコンパイルする場合、次のようにオプションを指定する必要があります。

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```