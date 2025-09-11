---
title: Fydetab Duo
description:
published: true
date: 2024-11-10T19:45:29.939Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# Fydetab Duo

このデバイスはCinnamon と KDE をサポートしていますが、ノームとの作業に対する回避策も利用できます。

# インストール

簡単に言うと、 `rkdeveloptool` を使って画像をeMMCにフラッシュします。 コマンドは次のとおりです: コマンドは次のとおりです:

```bash
# first, put the device in maskrom mode
# and flash the spi loader
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# then flash the os image
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

詳細な手順については、[📦 eMMCにインストールする方法](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro) を参照してください。

# 補助線

- [🐾 Mali GPUで RK3588をセットアップする方法](/how-to/how-to-setup-panthor)
- [🎮 ブレッドOSにSTEAMをインストールする方法](/how-to/how-to-install-steam)
- [🦶 FydetabのGNOME (/fydetab-duo/gnome)
- [📦 eMMCにインストールする方法](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [🔧 fydetabduo wikiの詳細情報](https://wiki.fydetabduo.com/category/-bredos)
