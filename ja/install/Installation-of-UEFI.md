---
title: UEFIのインストール
description:
published: false
date: 2025-09-16T12:36:51.696Z
tags:
editor: markdown
dateCreated: 2025-09-16T11:29:43.061Z
---

# 1. はじめに

サポートされている多くのデバイスは、ハードウェアを初期化してオペレーティングシステムを起動する最新のファームウェアインターフェースである`UEFI`をサポートしています。 `UEFI`の助けを借りてデバイスを起動することができます。 ファイル(USBスティックに書き込まれたり、DVDに書き込まれたり)、nVMEドライブから、またはPXEを介してネットワーク経由でOSを直接起動したりします。

# 2. お使いのデバイスを調べる

残念ながら、サポートしているすべてのデバイスが 'UEFI' をサポートしているわけではありません。 また、すべてのデバイスにSPIチップがインストールされているわけではありません。

- デバイスが何ができるかを判断するには、[this table](/en/table-of-supported-devices)をチェックしてください。

# 3. インストール

- UEFI ビルド [here](https://github.com/BredOS/edk2-rk3588/releases) の最新リリースをダウンロードします。

## 3.1 SDカードへのインストール

デバイスと一致する最新のリリースをダウンロードし、任意のサイズのSDカード(ほぼ)をライターに挿入し、お好みの点滅ツールを使用します。 以下の使用をお勧めします。

- [BalenaEtcher](https://etcher.balena.io/)
- [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager)

> SDカードをSBCに挿入すれば、うまくいきます。
> {.is-success}

## 3.2 SPIへのインストール

> 3.1をスキップした場合は、戻ります。 このステップはSPIチップに点滅するために必要です!
> あとで
> {.is-info} SDカードを取り外すことができます

> この手順はテストされていません。 正常に完了した場合は、DiscordまたはTelegramのチャンネルをご報告ください。
> {.is-warning}

以下の手順に従って、SPIチップに`UEFI`をインストールしてください。

- 最新リリースの「UEFI」をFAT32フォーマットのUSB-スティックにコピーし、SBCに接続します。
- SDカードから `UEFI` でボードを起動します。 If you have trouble to get into UEFI Settings check [this guide](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- コマンドラインインターフェースを入力するには、`Boot Manager` -> `UEFI Shell` に移動します。
- `map` コマンドを使用して、読み取り可能なパーティションをすべてリストします。 このコマンドは、すべてのパーティションを `fs0:`、`fs1:`の名前スキームでリストします。
- ファームウェア画像を含むUSB-スティックに移動し、ファイルシステム名を入力し、Enterキーを押してディレクトリを変更します。 どのファイルシステムを使用すべきかわからない場合は、ls fsX: を実行して内容を一覧表示します。
- `UEFI`をコマンドでSPIチップに書き込みます。

```
sf updatefile <FIRMWARE.img> 0x0
```

- SBCをパワーダウンし、SDカードを取り外します。

> 今、あなたのデバイスはすべての素敵なUEFIグッズが可能です!
> {.is-success}
