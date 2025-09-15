---
title: デバイス固有の画像を使用したインストール
description:
published: false
date: 2025-09-15T13:06.236Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36:27.362Z
---

# 1. はじめに

BredOS をインストールするために、当社は特定のデバイスのボックスから動作するように調整されたデバイス固有の画像を提供します。 これらの画像は、ISOイメージを介してインストールすることと区別されます。 ISOイメージを介したインストールはより一般的ですが、私たちが提供するdevicesupportを超えてサポートされています。

> 当社のダウンロードサイトでデバイスが見つからず、お使いのデバイスがUEFI経由の起動に対応している場合。 ISOのインストールを試してみてください。
> {.is-info}

# 2. ダウンロード

画像のダウンロードリンクは、 [website](https://bredos.org/download.html)にあります!

# 3. インストール

インストールはデバイスによって異なり、ブレッドOSをインストールしたい媒体が異なります。 このガイドでは、インストールについて説明します。

- `3.1 non-removable eMMC`
- `3.2 リムーバブルeMMCとSDカード`
- `3.3 nVME`

> 始める前に、お使いのデバイスで利用可能なオプションを確認してください!
> {.is-info}

## 3.1 取り外し不可能なeMMC

このために使用できるさまざまなオペレーティングシステムをカバーするために、インストールを取り外し不可能なeMMCに分割することにしました。

- Linux または macOS で eMMC の書き込み
- Microsoft Windows で eMMC の書き込み

## 3.2 取り外し可能な eMMC および SD カード

> ラズベリーOSの点滅に精通している場合は、これ以上の読み取りは必要ありません。 SDカードまたはeMMC、デバイス固有のブレッドOSイメージを取得し、お好みのツールでフラッシュします。
> {.is-info}

### 3.2.1 取り外し可能なeMMCを準備してください

> eMMC ストレージを使用していない場合は、 \`3.2.2 EMMC / SD カードの書き込みをスキップします。
> {.is-info}

#### 3.2.1.1 と uSD アダプター

eMMCは基本的にSBCに(ほとんどの場合)ハード配線されているSDカードであるため、eMMCをSDカードに変換するために接続できるアダプタがあります。
![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)
eMMCのコネクタをuSDアダプタにしっかりと押し、SDカードリーダーに接続します。
![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

#### 3.2.1.2 USB to eMMC アダプター

ほとんどの一般的に知られているUSBスティックは、eMMCストレージに基づいているので、USB-スティックでありながら取り外し可能なeMMCストレージを備えたそこにUSBからeMMCアダプタがあります。 これらはブレッドOSのフラッシュにも使用できます。
![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

### 3.2.2 eMMC / SD カードの書き込み

SDカードやeMMCをフラッシュするための無数のツールがあります。 このガイドでは、 `BalenaEtcher` と `Raspberry Pi Imager` について説明します。 両方のツールは、Linux、macOS、およびMicrosoft Windowsのサポートを提供します。 続行するには、下のガイドのいずれかを選択してください。

- BalenaEtcherでの書き込み
- Raspberry Pi Imager での書き込み

## 3.3 nVME

### 3.3.1 事前要件

NVMEドライブからの直接起動はデバイスではサポートされていないため、UEFIを別のメディアにインストールする必要があります。 UEFIが起動されると、nVMEドライブから直接起動することができます。 UEFIをSPIまたはSDカードにインストールするには、こちらのガイドに従ってください。

### 3.3.2 nVMEのフラッシュ

ドライブを直接またはUSBアダプタ経由でPCに接続します。 次に\`3.2のガイドの一つに従ってください。 EMMC / SDカードの書き込みを行い、NVMeドライブに適切なドライブ文字またはパスを使用してください。 点滅後、ドライブをSBCのnVMEポートに接続します。

### 3.3.3 ブートオーダー

UEFIはドライブを自分で拾うことができるはずです。 しかし、それが起動しようとするデバイスの順序は、ブートプロセスを遅くしたり、完全に失敗することさえあります(例えば。 あなたのネットワークにPXEサーバーがある場合)。 ブート順序を変更するには、この [guide](/en/how-to/change-default-boot-order-rk3588) に従ってください。

> インストールに成功したら[**First Setup**](/en/install/first-setup)
> {.is-success}
