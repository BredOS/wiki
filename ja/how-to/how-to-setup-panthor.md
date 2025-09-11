---
title: 🐾 マリGPUでRK3588を使ってパンターをセットアップする方法
description:
published: true
date: 2025-09-11T18:23:22.464Z
tags:
editor: markdown
dateCreated: 2024-08-31T15:03:26.994Z
---

# RK3588 🚀 でマリGPUでPanthorを有効にする

このガイドでは、Mali GPUのPanthorとVulkanをRK3588チップセットでボードに表示するための手順を説明します。

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

### 🌋 3. Vulkanを有効化

vulkanローダーとドライバーをインストールします:

```
sudo pacman -S vulkan-icd-loader vulkan-panfrost
```

### 🔁 4. システムを再起動

グラフィックを検証したい場合は、以下を実行できます。

```
sudo pacman -S inxi mesa-utils
inxi -G
```