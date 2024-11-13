---
title: カーネル改造中
description: null
published: true
date: 2024-11-11T12:14:07.650Z
tags: null
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# カーネル改造中

このガイドでは主にRK3588とlinux-rockchip-rkr3カーネルに焦点を当てます。
しかし、このガイドはほとんどが他のカーネルに引き継ぐべきです。

## BredOS カーネルリポジトリ

BredOS は、linux-rockchip カーネルフォークを格納します:
https://github.com/BredOS/linux-rockchip

rkr3 カーネルで使用されるブランチは `rk6.1-rkr3` です。
メインラインの variant は `rk-mainline` になります。

## BredOS kernel PKGBUILD

THe カーネルはビルドされており、PKGBUILD を使用してパッケージがあります:
https://github.com/BredOS/sbc-pkgbuilds

## 重要なディレクトリ

`sbc-pkgbuilds` リポジトリ内には、 `linux-rockchip-rkr3` という名前のフォルダがあります。
ビルド中はカレント作業ディレクトリとして使用する必要があります。
