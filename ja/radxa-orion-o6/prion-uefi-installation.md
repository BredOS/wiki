---
title: Orion O6でUEFIを更新中
description:
published: false
date: 2025-09-17T07:50:57.353Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:45:47.183Z
---

# 1. はじめに

このガイドでは、Radxa Orion O6 `UEFI` ファームウェアを BredOS 1 にアップデートする方法について説明します。

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
- `3.2 インプレースアップデート` -> FAT32 フォーマットされた USB スティック
- `3.3 Update through flasher` -> A CH341A flasher

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

\*Prions \* `UEFI` の起動に問題がある場合や、以下の手順に従ってフラッシャーを使用することをお勧めします。

> フラッシャーが**1.8ボルト**に設定されていることを確認してください！
> {.is-warning}

### 3.3.1 Prepare

- `flashrom`ツールをインストールします。

 ```
 sudo pacman -S flashrom
 ```

- UEFI .zip ファイルを解凍し、UEFI バイナリ ファイルのサイズを特定します。

```
du ./cix_flash_all.bin
```

- 出力のサイズはバイト単位で表示されます。

```
6288062 ./cix_flash_all.bin
```

上の例では、ファイルサイズは `6288062` です。

- チップの仕様に合わせるには、ファイルの最後に "0" を追加する必要があります。 `<your file size here>`を上記のコマンドのファイルサイズに置き換えます。

```
dd if=/dev/zero bs=1 count=$(((8388608 - <your file size here>)) >> ./cix_flash_all.bin
```

> ファイルサイズをメモしてください。 アップデートによりサイズが異なる場合がありますので、上記からコピー&ペーストしないでください!
> {.is-info}

### 3.3.2 SPIに接続

> SPIチップを取り外す際に、ボードが電源から切断されていることを確認してください!
> {.is-warning}

プリオンのSPIチップは簡単に取り外せるようにソケットされています。 ソケットは CPU ファンヘッダーと GPIO ポートの間にあります。

- プリオンからSPIチップを取り外します。
- ZIFボードをフラッシャーに接続します。
- ピン1にはチップ上にドットが付いています。 フラッシャーのUSBポートが向いている間、ピン1は左上側にあります。 向きを右に取得するには、以下のスクリーンショットを参照してください:

![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)

- フラッシャーをPCに接続し、次のように書き込みを開始します。

```
sudo flash -p ch341a_spi -w ./cix_flash_all.bin 
```

- "VERIFIED"という文字が表示された場合は、ファームウェアが正しく書き込まれています。