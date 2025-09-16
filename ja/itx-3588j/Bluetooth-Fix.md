---
title: Bluetooth Fix (ITX-3588J)
description:
published: true
date: 2025-09-16T10:51:52.361Z
tags:
editor: markdown
dateCreated: 2025-09-14T11:10:38.109Z
---

# Bluetooth Fix (ITX-3588J)

## 1. r58x-post-installをインストール

今のところ、パッケージを別のものに置き換える必要があります。 今のところ、パッケージを別のものに置き換える必要があります。 これは itx-3588j の動作を変更せず、ブート時に bluetoothを修正するサービスを追加します。

- 最初に `itx-3588j-post-install` を削除します。 このパッケージはスタンバイ問題を回避するために必要なパラメータを設定します。 私たちは再びこれを修正しないでください。 このパッケージはスタンバイ問題を回避するために必要なパラメータを設定します。 私たちは再びこれを修正しないでください。

```
sudo pacman -R itx-3588j-post-install
```

- その後、 `r58x-post-install` をインストールします。 このパッケージは上記と同じようにスタンバイしますが、 `bluetooth-mekotronics` サービスが含まれています。 このパッケージは上記と同じようにスタンバイしますが、 `bluetooth-mekotronics` サービスが含まれています。

```
sudo pacman -S r58x-post-install
```

## 2. 正しいUARTパスを設定

Bluetooth アダプターは `/dev/ttyS9` に接続されていません (他の RK3588 SBC のように)、`/dev/ttyS6` に接続されています。 `/usr/bin/bluetooth-fix` 内のパスを変更する必要があります。

- `/usr/bin/bluetooth-fix` 内のパスを変更する必要があります。

```
sudo nano /usr/bin/bluetooth-fix
```

```
#! /bin/bash

/usr/sbin/rfkill block 0
/usr/sbin/rfkill block bluetooth
/bin/sleep 2
/usr/sbin/rfkill unblock 0
/usr/sbin/rfkill unblock bluetooth

# FIXME Delay
/bin/sleep 1

brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS9
```

- 最後の行を `/dev/ttyS6` に変更します。

```
brcm_patchram_plus --enable_hci -no2bytes --use_baudrate_for_download --tosleep 200000 --baudate 1500000 --patchram /lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS6
```

## 3. Bluetooth サービスを有効にする

- 最後に `bluetooth-mekotronics` サービスを有効にする必要があります

```
sudo systemctl --now enable bluetooth-mekotronics
```

> 以上です！ 以上です！ Bluetoothは今正常に動作するはずです。
> {.is-success}
> {.is-success}
