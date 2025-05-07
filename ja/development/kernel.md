---
title: カーネル改造中
description: null
published: true
date: 2025-05-07T13:13:10.144Z
tags: null
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# カーネル改造中

このガイドでは、主に RK3588 と `linux-rockchip-rkr3` カーネルに焦点を当てます。
しかし、このガイドはほとんどが他のカーネルに引き継ぐべきです。

## BredOS カーネルリポジトリ

BredOS は `linux-rockchip` カーネルフォークを格納します:
https://github.com/BredOS/linux-bredos

rkr3 カーネルで使用されるブランチは `rk6.1-rkr3` です。
メインラインの variant は `rk-mainline` になります。

## BredOS kernel PKGBUILD

カーネルはビルドされており、PKGBUILD のパッケージは
https://github.com/BredOS/sbc-pkgbuilds

## カーネルのビルド

ARMシステムの下で, just :

```bash
make -j$(nproc)
```

x86システムでは、カーネルをクロスコンパイルする必要があります。

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

`arch/arm64/boot/`ディレクトリに画像が表示されます。

## 重要なディレクトリ

`sbc-pkgbuilds` リポジトリ内には、 `linux-rockchip-rkr3` という名前のフォルダがあります。
ビルド中はカレント作業ディレクトリとして使用する必要があります。

## デバイスツリーとオーバーレイのコンパイル

`dtsc`を使用するための完全なガイドが、DTBとDTBOをコンパイルするためのブレッドOSツールが利用可能になりました。
[here](/en/how-to/dtsc) をクリックして表示します。