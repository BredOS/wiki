---
title: Microsoft Windows で eMMC の書き込み
description:
published: false
date: 2025-09-18T08:59:46.182Z
tags:
editor: markdown
dateCreated: 2025-09-16T09:55:34.272Z
---

# 1. はじめに

何よりもまず、Windowsを使用する必要があると聞いて申し訳ありません。
しかし、恐れはありません - とにかくあなたをカバーしています。
この記事では、 `RKDevTool` と必要な `RockChip Maskromドライバ` をインストールするプロセスを説明します。

BredOS のインストールには、以下の4つのものが必要です:

1. SPI loader file for example, for the RK3588: [`rk3588_spl_loader_v1.15.11.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.11.bin)
2. Device Specific Image from our [official website](https://bredos.org/download.html)
3. [RockChip Maskrom drivers](https://dl.radxa.com/tools/windows/)
4. [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool), [Alternative Link 1](https://dl.radxa.com/tools/windows/)

# 2) ドライバ

We start with the installation of the [Rockchip Driver](https://dl.radxa.com/tools/windows/DriverAssitant_v5.0.zip). その.zipファイルをダウンロードした後、それをあなたの好みの場所に抽出します。
内部には、ツール「DriverInstall.exe」があります。 権利を高めて実行します。

> 「このアプリでデバイスに変更を許可しますか？」と聞かれた場合は、「はい」をクリックします。
> {.is-info}

ウィンドウがポップアップします。 `Install Driver`をクリックします。 ドライバはシステムにインストールされます。

# 3. RKDevToolを使ってブレッドOSをフラッシュする

所定の場所にあるドライバでは、 [RKDevTool](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool) の使用を続けることができます。 .zip ファイルを抽出し、`RKDevTool.exe` を実行します。

`RKDevTool` で次の設定を行い、`RUN`をクリックします。

- SoCに対応するSPIローダーファイルを選択します。
- SBCのブレッドOSイメージ (.img) を選択します。
- `アドレスで書く` にチェックを入れます。
- `RUN`をクリックして、プロセスが終わるまで待ちます。

> 画像は .xz 圧縮ファイルとして提供します。 書き込みの前に含まれている .img ファイルを抽出する必要があります。
> {.is-warning}

それが点滅プロセスを終えるのを待ち、あなたは行くのが良いです。

> フラッシュに成功したら[**最初のセットアップ**](/en/install/first-setup)で続行します。
> {.is-success}