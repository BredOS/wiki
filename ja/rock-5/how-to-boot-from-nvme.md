---
title: NVMeドライブから起動する方法
description: このガイドでは、NVMeドライブからの起動をセットアップする方法を説明します
published: true
date: 2025-09-17T10:09:37.865Z
tags: rock-5, rock-5b, rock-5bp, nvme
editor: markdown
dateCreated: 2024-09-21T09:09:29.723Z
---

# 1. はじめに

Rock 5BまたはRock 5B PlusのNVMe SSDからBredOSを起動する いくつかの手順に従ってデバイスを準備する必要があります

これらの手順は、Rock 5B/5B PlusがすでにLinux(eMMCまたはmicroSDカードのいずれか)に起動され、ネットワーク接続性があることを前提としています。 オフラインの場合は、USBスティックのように必要なファイルを外部メディアにコピーしてアクセスします。 オフラインの場合は、USBスティックのように必要なファイルを外部メディアにコピーしてアクセスします。

# 2. インストール

## 2.1 UEFI ファームウェアの更新

まず、最新のUEFIファームウェアがインストールされていることを確認してください。 BredOS リポジトリから必要なパッケージを簡単にインストールできます。 BredOS リポジトリから必要なパッケージを簡単にインストールできます。

- **Rock 5B**の場合は、次のコマンドを使用します。

```bash
sudo pacman -Sy rock-5b-uefi
```

- **Rock 5B Plus**の場合は、次のようにします。

```bash
sudo pacman -Sy rock-5bplus-uefi
```

## 2.2 フラッシュUEFIからSPIへ

次に、UEFIファームウェアをデバイスのSPIメモリにフラッシュする必要があります。

- **Rock 5B Plus**の場合は、次のコマンドを使用します。

```bash
sudo dd if=/usr/share/edk2/rock-5bplus/rock-5bplus_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

- **Rock 5B**の場合は、次のようにします。

```bash
sudo dd if=/usr/share/edk2/rock-5b/rock-5b_UEFI_Release_latest.img of=/dev/mtdblock0 bs=512 skip=64 seek=64 conv=notrunc
```

## 2.3 BredOS イメージを NVMe に書き込みます

UEFI が書き込まれたら、最新の BredOS イメージを [Images](https://github.com/BredOS/images/releases) リポジトリからダウンロードする必要があります。 イメージファイルを抽出し、`dd`コマンドを使用してNVMe SSDにイメージを書き込みます。 イメージファイルを抽出し、`dd`コマンドを使用してNVMe SSDにイメージを書き込みます。

- `/dev/nvme0n1`をNVMeドライブへの正しいパスに置き換えてください。

```bash
sudo dd if =/path/to/bredos_image.img of=/dev/nvme0n1 bs=4M status=progress
```

> NVMeから起動する際にSDカードやEMMCを接続しないでください。デバイスが起動しないようにします。
> {.is-warning}
> {.is-warning}

> 処理が完了したら、Rock 5B/5B Plusを再起動し、NVMe SSDから起動します!
> {.is-success}
