---
title: BredOS のインストールガイド
description:
published: true
date: 2025-09-24T12:13:46.662Z
tags:
editor: markdown
dateCreated: 2024-07-19T00:42:37.505Z
---

# 🔄 1. BredOS インストールガイド

あなたのためにインストールを容易にするために、私たちはあなたが従うように交配されたパン粉のラインをレイアウトしました。 🍞 🔸🔸🔸 🍞 🔸🔸🔸

## 1.1 デバイス固有の画像のインストール

These are the boards we love the most. これらは、私たちが最も好きなボードのための画像です。 To install this BredOS images on them, either start with our [device specific image](/install/device-specific-image) installation guide, or take a glimpse to the device page at our wiki, which can be found in the navigation bar left of this.

私たちの[ダウンロードサイト](https://bredos.org/download.html)にアクセスして、お使いのデバイスがそのうちの1つであるかどうかを確認してください。

## 1.2 一般的なインストール

If your device isn’t listed on our [download site](https://bredos.org/download.html) but supports booting UEFI and is based on either x86- or ARM64 architecture, simply follow our guide for a generic installation available [here](/install/Installation-with-ISO).

## 1.3 Docker コンテナーのインストール

- コマンドの一行として簡単:

```

docker pull bredos/bredos

```