---
title: Fydetab Duo
description:
published: true
date: 2025-09-17T10:16:17.074Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:37:43.624Z
---

# 1. はじめに

Fydetab DuoはFyde Innovationsによって開発された2イン1錠です。 FydeOSのメーカーであるChromium-OSベースのシステム(Linux系)で、Androidアプリを実行することもできます。 タブレットとして、または取り外し可能なキーボード/ケース + スタイラスを使用して、小さなラップトップのように機能するように設計されています。 タブレットとして、または取り外し可能なキーボード/ケース + スタイラスを使用して、小さなラップトップのように機能するように設計されています。

キーの仕様:

- ディスプレイ:12.35′′IPSパネル、解像度〜2560×1600、明るさ〜500ニット。
- プロセッサ: ARMベースのRockchip RK3588S SoC。
- メモリとストレージ:8 GB LPDDR4X RAM。 ストレージは128 GB eMMCです。 microSD を介して拡張できます。 microSD を介して拡張できます。
- バッテリー:<unk> 42Wh、推定バッテリ寿命まで〜10時間。
- その他の機能:Wi-Fi 6、Bluetooth 4.2、指紋センサー、ステレオスピーカー、5 MPフロントカメラ、スタイラス対応。

> 私たちはそれを「_FydeTube_」、「_FDT_」、または「_Duo_」とあだ名し、あなたの選択を取ります。
> {.is-info}
> {.is-info}

# 2. ダウンロード

画像のダウンロードリンクは、 [website](https://bredos.org/download.html)にあります!

# 3. インストール

- 簡単に言うと、 `rkdeveloptool` を使って画像をeMMCにフラッシュします。 コマンドは次のとおりです: コマンドは次のとおりです:

```bash
# first, put the device in maskrom mode
# and flash the spi loader
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
# then flash the os image
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

詳細な手順については、[📦 eMMCにインストールする方法](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro) を参照してください。

# 4. 有用なリンク

- [🐾 Mali GPUで RK3588をセットアップする方法](/how-to/how-to-setup-panthor)
- [🎮 ブレッドOSにSTEAMをインストールする方法](/how-to/how-to-install-steam)
- [Switch Desktop Environment](/en/how-to/switch-desktop-environments)
- [📦 eMMCにインストールする方法](https://wiki.fydetabduo.com/os-release-board/BredOS/BredOS-intro)
- [🔧 fydetabduo wikiの詳細情報](https://wiki.fydetabduo.com/category/-bredos)
