---
title: 🐾 マリGPUでRK3588を使ってパンターをセットアップする方法
description:
published: true
date: 2025-07-22T00:13:05.435Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# RK3588 🚀 でマリGPUでPanthorを有効にする

このガイドでは、RK3588チップセットを搭載したボードに搭載されているMali GPUでPanthorを有効にするための手順を説明します。

# 🔧 パンターを有効にする手順

### 🎛️ 1. Panthor DTBO を有効にする

[Device Tree Overlay guide](/how-to/how-to-enable-dtbos)に従って、
`/boot/dtbs/rockchip/overlay/rockchip-rk3588-panthor-gpu.dtbo`
**DTBOをコピーした後、システムを再起動しないでください！**

### 🔄 2. Panfork グラフィックスを置き換え

`mesa-panfork-git` パッケージを標準の `mesa` パッケージに置き換えます。

```
sudo pacman -S mesa
```

### 🔁 3. システムを再起動

グラフィックを検証したい場合は、以下を実行できます。

```
sudo pacman -S inxi mesa-utils
inxi -G
```