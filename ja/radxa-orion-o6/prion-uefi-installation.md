---
title: Orion O6でUEFIを更新中
description:
published: false
date: 2025-09-17T06:45:47.183Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. はじめに

このガイドでは、Radxa Orion O6 `UEFI`ファームウェアをBredOSにアップデートするプロセスについて説明します。

# 2. 特徴

- フロントパネルのUSBポートを固定しました
- CPU速度は2.6GHzで実際に動作するように固定されています
- ACPI の修正
- Bluetooth/wifiカードの修正
- M.2 ssds does dissapear random
- `UEFI`解像度修正

# 3. インストール

## 3.1 前提条件

- `UEFI`インストール.zipファイル
- 場所内の更新の場合 -> FAT32 フォーマットされた USB スティック
- フラッシャー経由で更新する場合-> A CH341A based flasher

https://www.aliexpress.com/item/32263275388.html
![spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> リンクの有効期限が切れた場合は、DiscordまたはTelegramからお気軽にご連絡ください。

## 3.2 現場での更新

以下の手順に従って、 `UEFI` ファームウェアを Radxa UEFI 内からインストールできます。

- USBスティックをFAT32にフォーマットし、zipファイルの内容をドライブのルートディレクトリに配置します。
- USBスティックの内容は以下のように表示されます:

```
BuildOptions  
BurnImage.efi  
cix_flash_all.bin  
cix_flash_ota.bin  
FlashUpdate.efi  
Shell.efi  
startup.nsh  
VariableInfo.efi
```

- ボードを `UEFI` で起動します。 If you have trouble accessing the UEFI Settings, check [this guide](/en/how-to/change-default-boot-order-rk3588#2.1-Accessing-the-Boot-Menu).
- コマンドラインインターフェースを入力するには、`Boot Manager` -> `UEFI Shell` に移動します。
- 更新プロセスが自動的に開始されます。

> アップデートに成功した後、ボードをシャットダウンし、電源から少なくとも10秒間取り外します!
> {.is-warning}

## 3.3 フラッシャーによるアップデート
