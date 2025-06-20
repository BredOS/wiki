---
title: BredOS のインストールガイド
description:
published: true
date: 2024-08-16T10:06:04.691Z
tags:
editor: markdown
dateCreated: 2024-07-19T00:42:37.505Z
---

# 🍞 BredOS インストールガイド

## 📚 目次の項目

- [🔽 BredOSのダウンロード](#downloading-bredos)
- [💽 インストールメディアの作成 (microSD)](#creating-the-installation-media-microsd)
- [🚀 インストール メディア (microSD)からの起動](#booting-from-the-installation-media-microsd)
- [💾 eBredOS を eMMC (RockChip)にインストールする](#installing-bredos-to-emmc-rockchip)
- [💻 BredOS インストーラをフォロー](#follow-bredos-installer)
- [🛠️ 初期設定](#initial-configuration)

## 🔽 BredOS のダウンロード

[🌐 official website](https://bredos.org/download.html)からデバイスの最新のブレッドOS画像をダウンロードしてください。

## 💽 インストールメディアの作成 (microSD)

1. microSDカードをコンピュータに挿入します。
2. [`balenaEtcher`](https://etcher.balena.io/), `dd`, または [`Raspberry Pi Imager`](https://www.raspberrypi.com/software/) のようなツールを使用して、ブレッドOSイメージをmicroSDカードに書き込みます。

## 🚀 インストールメディアからの起動 (microSD)

1. ARMベースのシングルボードコンピュータにmicroSDカードを挿入します。
2. 必要な周辺機器(キーボード、マウス、モニター)と電源をデバイスに接続します。
3. デバイスはmicroSDカードから起動し、ブレッドOSインストーラをロードする必要があります。

## 💾 eBredOS を eMMC (RockChip) にインストールする

microSD カードの代わりに BredOS を eMMC ストレージにインストールする場合は、以下の手順に従ってください。

**📝 始める前に以下のファイルがダウンロードされていることを確認してください:**

- [📥 Rockchip Driver](https://dl.radxa.com/tools/windows/DriverAsitant_v5.0.zip)

- 書き込みツール **(RKDevTool vX.XX)**: 以下のリンクからWindows用のツールをダウンロードできます。
    - [🔗 Link 1](https://docs.radxa.com/en/compute-module/cm5/radxa-os/low-level-dev/rkdevtool)
    - [🔗 Alternative in case `Link 1` doesn't work](https://dl.radxa.com/tools/windows/)
    - [🔗 Link to version v2.96](https://dl.radxa.com/tools/windows/RKDevTool_Release_v2.96_zh.zip)

- SPI loader file for example, for the RK3588: [`rk3588_spl_loader_v1.15.11.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.11.bin)

- format@@0(#downloading-bredos).

**📂 デフォルトでBredOSイメージを含むすべてのファイルを解凍します。 mg.xzファイルを解凍して.imgファイルに変換する必要があります。**

- まず最初に、ダウンロードしたRockchipドライバをインストールすることです。 これを行うには、`DriverAsitant_v5.0`フォルダを開き、`DriverInstall.exe`ファイルを実行します。

- `🟢 Driverをインストール`をクリックします:

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Android/AOSP/install_drivers.png)

- 書き込みツールが含まれるフォルダを開きます: `RKDevTool_Release_v2.96` フォルダ(ダウンロードした名前のバージョンを確認してください) そしてツール`RKDevTool.exe`を実行します。

- 点滅ツールで次の設定を行い、`RUN`をクリックします。
    - SPIローダーファイルを選択してください
    - BredOS の画像を選択
    - 「アドレスで書く」をチェックします。
    - `RUN`をクリックして、プロセスが終了するまで待ちます。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/flashing_tool_config.png)

Linuxユーザーの場合、`rkdeveloptool` を使用してイメージをeMMCにフラッシュすることができます。 コマンドは次のとおりです:

```bash
sudo rkdeveloptool db ~/Downloads/rk3588_spl_loader_v1.09.111.bin
sudo rkdeveloptool wl 0 ~/Downloads/BredOS.img
```

## 💻 BredOS インストーラをフォローする

1. 画面の指示に従ってインストールプロセスを完了します。
2. 言語、キーボードレイアウト、およびタイムゾーンを選択します。
3. ユーザーアカウントとパスワードを設定します。
4. インストールを完了し、デバイスを再起動します。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/breDOS_installer.jpg)

## 🛠️ 初期設定

BredOS インストーラを実行した後、初期設定タスクを完了する必要があります。

- 🌐 ネットワーク設定を構成する
- 🔄 パッケージマネージャを使用してシステムを更新する
- 🛠️ 必要に応じて追加のソフトウェアパッケージをインストールする

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg