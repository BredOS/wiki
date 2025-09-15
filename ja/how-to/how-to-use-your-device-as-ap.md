---
title: ワイヤレスホットスポットとしてデバイスを使用する方法
description:
published: true
date: 2025-09-15T09:43:47.485Z
tags:
editor: markdown
dateCreated: 2024-09-08T10:33:46.772Z
---

# 1. はじめに

このガイドではNetworkManagerを使用してWi-Fiホットスポットを設定する方法を説明します。

# 2. 前提条件

始める前に、以下の内容を確認してください:

- AP (アクセス ポイント) モードをサポートする Wi-Fi アダプター

> AP (アクセス ポイント) モードをサポートする適切なデバイスには、Rock 5C、Rock 5B+、が含まれます。 Khadas Edge 2, Khadas Vim 4, Mekotronics R58デバイス, Orange Pi 5B.
> {.is-info}

# 3. インストール

## 3.1 ホットスポットを作成

NetworkManager のコマンド ライン ツール `nmcli` を使用すると、簡単にホットスポットを作成できます。

- 使用するWi-Fiインターフェイスを識別するためにネットワークデバイスをリストアップします:

  ```bash
  nmcli デバイスの状態
  ```

- 次のコマンドを使用してホットスポットを作成します。

  ```bash
  nmcli デバイス wifi hotspot ifname <wifi_interface> ssid <MyHotspot> パスワード <mypassword>
  ```

  Replace `<wifi_interface>` with your actual interface name, like `wlp2s0` or `wlan0`,  `<MyHotspot>` with your desired SSID and `<mypassword>` with a secure passphrase of your choice.

> If you get the following error run the command again with sudo
> `Error: Failed to setup a Wi-Fi hotspot: Not authorized to control networking.`
> {.is-info}

## 3.2 ホットスポットの状態を表示

- ホットスポットが作成されると、次を実行してステータスを確認できます。

```bash
nmcli 接続ショー
```

アクティブな接続の下にホットスポットが表示されます。

## 3.3 IP 転送を設定する

ホットスポット経由でインターネット接続を共有するには、IP転送を有効にする必要があります。

- IP転送を有効にする:

  ```bash
  sudo sysctl net.ipv4.ip_forward=1
  ```

- `/etc/sysctl.d/99-sysctl.conf`を編集することで永続化します。

  ```bash
  sudo nano /etc/sysctl.d/99-sysctl.conf
  ```

- 次の行を追加:

  ```
  net.ipv4.ip_forward=1
  ```

## 3.4 ホットスポットの停止

- ホットスポットを停止するには、以下を実行します。

```bash
nmcli connection down Hotspot
```
