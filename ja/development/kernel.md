---
title: カーネル改造中
description:
published: true
date: 2025-05-07T18:34:49.447Z
tags:
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# 1. BredOS カーネルリポジトリ

このガイドでは、主に RK3588 と `linux-rockchip-rkr3` カーネルに焦点を当てます。
しかし、このガイドはほとんどが他のカーネルに引き継ぐべきです。
しかし、このガイドはほとんどが他のカーネルに引き継ぐべきです。

# 2. BredOS kernel PKGBUILD

## 2.1 BredOS カーネルリポジトリ

BredOS は `linux-rockchip` カーネルフォークを格納します:
https://github.com/BredOS/linux-bredos

rkr3 カーネルで使用されるブランチは `rk6.1-rkr3` です。
メインラインの variant は `rk-mainline` になります。
rkr3 カーネルで使用されるブランチは `rk6.1-rkr3` です。
メインラインの variant は `rk-mainline` になります。
rkr3 カーネルで使用されるブランチは `rk6.1-rkr3` です。
メインラインの variant は `rk-mainline` になります。
メインラインの variant は `rk-mainline` になります。

## 2.2 BredOS kernel PKGBUILD

カーネルはビルドされており、PKGBUILD のパッケージは
https://github.com/BredOS/sbc-pkgbuilds

## 2.3 カーネルのビルド

- ARMシステムの下で, just :

```bash
make -j$(nproc)
```

- x86システムでは、カーネルをクロスコンパイルする必要があります。

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

`arch/arm64/boot/`ディレクトリに画像が表示されます。

> `sbc-pkgbuilds` リポジトリ内には、 `linux-rockchip-rkr3` という名前のフォルダがあります。
> ビルド中はカレント作業ディレクトリとして使用する必要があります。
> ビルド中はカレント作業ディレクトリとして使用する必要があります。
> {.is-info}

# 3. デバイスツリーとオーバーレイのコンパイル

`dtsc`を使用するための完全なガイドが、DTBとDTBOをコンパイルするためのブレッドOSツールが利用可能になりました。
[here]/Tools#dtsc-helper-script) をクリックして表示します。
[here](/Tools#dtsc-helper-script) をクリックして表示します。