---
title: デバイス固有の画像を使用したインストール
description:
published: true
date: 2025-10-22T08:35:52.202Z
tags:
editor: markdown
dateCreated: 2025-09-15T12:36:27.362Z
---

# 1. はじめに

BredOS をインストールするために、当社は特定のデバイスのボックスから動作するように調整されたデバイス固有の画像を提供します。 これらの画像は、ISOイメージを介してインストールすることと区別されます。 ISOイメージを介したインストールはより一般的ですが、私たちが提供するdevicesupportを超えてサポートされています。 これらの画像は、ISOイメージを介してインストールすることと区別されます。 ISOイメージを介したインストールはより一般的ですが、私たちが提供するdevicesupportを超えてサポートされています。 これらの画像は、ISOイメージを介してインストールすることと区別されます。 ISOイメージを介したインストールはより一般的ですが、私たちが提供するdevicesupportを超えてサポートされています。

> ラズベリーOSの点滅に精通している場合は、これ以上の読み取りは必要ありません。 SDカードまたはeMMC、デバイス固有のブレッドOSイメージを取得し、お好みのツールでフラッシュします。
> {.is-info} Just grab your SD-Card or eMMC, your device specific image and flash with your preferred Tool.
> {.is-info}

# 2. ダウンロード

画像のダウンロードリンクは、 [website](https://bredos.org/download.html)にあります!

# 3. ブートデバイス

- BredOS をインストールしたいストレージデバイスを選択してください：

### Tabset {.tabset}

#### SD カード

<details><summary><b>SD Card Adapter</b></summary>

PCのSDカードリーダーにSDカードを挿入し、[**4.1 with Storage Adapter**](#h-41-with-storage-adapter) を続けてください。

</details>

<details><summary><b>SD Card Adapter</b></summary>

SDカードをSBCに挿入し、[**4.2 with RKdeveloptool**](#h-4-2-with-rkdeveloptool)のセクションにあるPCのOSに従ってガイドを続行します。

> 点滅する前に、ターゲットデバイスを `sd card` に設定する必要があります。 そのためには、[4.2 フラッシュターゲットの変更](/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS#h-42-changing-flash-target)を見てください。
> {.is-info}

</details>

#### 削除できないeMMC

<details><summary><b>RKdeveloptool</b></summary>

[**4.2 with RKdeveloptool**](#h-4-2-with-rkdeveloptool) にあるPCのOSに従ってガイドを続行します。

</details>

#### 取り外し可能なeMMC

<details><summary><b>EMMC対USBアダプタ</b></summary>

ほとんどの一般的に知られているUSBスティックは、eMMCストレージに基づいているので、USB-スティックでありながら取り外し可能なeMMCストレージを備えたそこにUSBからeMMCアダプタがあります。 これらはブレッドOSのフラッシュにも使用できます。 これらはブレッドOSのフラッシュにも使用できます。 これらはブレッドOSのフラッシュにも使用できます。 これらはブレッドOSのフラッシュにも使用できます。 以下のスクリーンショットに示すように、eMMCをアダプターに接続します。

<details>3.2.1.2 USB to eMMC アダプター

![emmc-reader-cut.png](/installation-dsi/emmc-reader-cut.png)

   </details>

[**4.1 with Storage Adapter**](#h-41-with-storage-adapter) を続行します。

</details>

<details><summary><b>USD アダプター</b></summary>
eMMCは基本的にSBCに(ほとんどの場合)ハードワイヤードされたSDカードであるため、eMMCを接続してSDカードに変換できるアダプターがあります。

<details><summary><b>uSD Adpater と eMMC</b></summary>

![usd-emmc-cut.png](/installation-dsi/usd-emmc-cut.png)

</details>
Firmly press the connector of the eMMC onto the uSD Adapter and connect them to your SD Card Reader.

<details><summary><b>uSD アダプターがリーダー</b></summary> に接続されています

![usd-connected-cut.png](/installation-dsi/usd-connected-cut.png)

</details>

[**4.1 with Storage Adapter**](#h-41-with-storage-adapter) を続行します。

</details>

<details><summary><b>Without Adapter</b></summary>

あなたのSBCにeMMCを接続し、セクション[**4.2 with RKdeveloptool**](#h-4-2-with-rkdeveloptool)にあるPCのOSに従ってガイドを続行します。

</details>

#### NVMe

> NVMeドライブからの直接起動はデバイスではサポートされていないため、UEFIを別のメディアにインストールする必要があります。 UEFIが起動されると、nVMEドライブから直接起動することができます。 To install UEFI to your SPI or SD Card follow this guide. UEFIが起動されると、NVMeドライブから直接起動することができます。 UEFIが起動されると、nVMEドライブから直接起動することができます。 To install UEFI to your SPI or SD Card follow this guide.
> {.is-warning}

<details><summary><b>USBアダプタ</b></summary>

USBアダプタを介してドライブをPCに接続し、[**4.1 with Storage Adapter**](#h-41-with-storage-adapter)を続行します。 ドライブを直接またはUSBアダプタ経由でPCに接続します。 ドライブを直接またはUSBアダプタ経由でPCに接続します。 次に、[3.2] で推奨されるツールのいずれかを使用します。 EMMC / SDカードの書き込み](#h-322-flashing-emmc-sd-card)、NVMeドライブの正しいドライブ文字またはパスを使用してください。 点滅後、ドライブをSBCのnVMEポートに接続します。 点滅後、ドライブをSBCのNVMeポートに接続します。

</details>

<details><summary><b>Without Adapter</b></summary>

NVMeドライブをPCに直接接続し、[**4.1 with Storage Adapter**](#h-41-with-storage-adapter)を続行します。 ハードドライブに書き込むには、フラッシュツールを強制する必要があります。

</details>

# 🚀 4. フラッシュ中

> .xz ファイルとして圧縮された画像を提供します。 点滅する前にそれらを解凍してください! 点滅する前にそれらを解凍してください!
> これを実行することはできません！
> {.is-warning}
> {.is-warning}

## 4.1 ストレージアダプター付き

SDカードやeMMCをフラッシュするための無数のツールがあります。 `BalenaEtcher` または `Raspberry Pi Imager` を使用することをお勧めします。 両方のツールは、Linux、macOS、およびMicrosoft Windowsのサポートを提供します。 `BalenaEtcher` または `Raspberry Pi Imager` を使用することをお勧めします。 両方のツールは、Linux、macOS、およびMicrosoft Windowsのサポートを提供します。 `BalenaEtcher` または `Raspberry Pi Imager` を使用することをお勧めします。 両方のツールは、Linux、macOS、およびMicrosoft Windowsのサポートを提供します。 `BalenaEtcher` または `Raspberry Pi Imager` を使用することをお勧めします。 両方のツールは、Linux、macOS、およびMicrosoft Windowsのサポートを提供します。

- [BalenaEtcher](https://etcher.balena.io/)
- Raspberry Pi Imager での書き込み

## 4.2 rKdeveloptool

このために使用できるさまざまなオペレーティングシステムをカバーするために、以下の2つのガイドにインストールを分割することにしました:

- [Flashing with RKDevelop under Linux or macOS](/en/install/device-specific-image/Flashing-the-eMMC-with-Linux-or-macOS)
- [Flashing with RKDevelop under Microsoft Windows](/en/install/device-specific-image/Flashing-the-eMMC-with-Microsoft-Windows)
