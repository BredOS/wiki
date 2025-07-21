---
title: ":antera_bars: デバイスを無線ホットスポットとして使用する方法"
description:
published: true
date: 2024-09-08T14:15:47.669Z
tags:
editor: markdown
dateCreated: 2024-09-08T10:33:46.772Z
---

# :antera_bars: NetworkManager を使用してホットスポットを設定する方法

このガイドではNetworkManagerを使用してWi-Fiホットスポットを設定する方法を説明します。

## 🛠️ 前提条件

始める前に、以下の内容を確認してください:

- :satellite_アンテナ: AP (アクセス ポイント) モードをサポートする Wi-Fi アダプター

> AP (アクセス ポイント) モードをサポートする適切なデバイスには、Rock 5C、Rock 5B+、が含まれます。 Khadas Edge 2, Khadas Vim 4, Mekotronics R58デバイス, Orange Pi 5B.
> {.is-info}

## 🚀 ホットスポットを作成

NetworkManager のコマンド ライン ツール `nmcli` を使用すると、簡単にホットスポットを作成できます。

1. **ネットワーク機器のリスト**を使って、Wi-Fiインターフェースを識別します：

   ```bash
   nmcli デバイスの状態
   ```

2. \*\*以下のコマンドを使用してホットスポットを作成します（`wlp2s0`や`wlan0`のような実際のインターフェイス名に`wifi_interface`を置き換えます）：

   ```bash
   nmcli デバイス wifi hotspot ifname wifi_interface ssid MyHotspot password "mypassword"
   ```

   このコマンドは次のとおりです。

   - 📝 SSID `MyHotspot` でホットスポットを作成する
   - 🔑 パスワードを `mypassword` に設定する

> If you get the following error run the command again with sudo
> `Error: Failed to setup a Wi-Fi hotspot: Not authorized to control networking.`
> {.is-info}

## 🔍 ホットスポットの状態を表示

ホットスポットが作成されると、次を実行してステータスを確認できます。

```bash
nmcli 接続ショー
```

アクティブな接続の下にホットスポットが表示されます。

## 🌐 IP 転送を設定する

ホットスポット経由でインターネット接続を共有するには、IP転送を有効にする必要があります。

1. **IP転送を有効化**:

   ```bash
   sudo sysctl net.ipv4.ip_forward=1
   ```

2. **`/etc/sysctl.d/99-sysctl.conf`を編集することで**恒久的に**します** ：

   ```bash
   sudo nano /etc/sysctl.d/99-sysctl.conf
   ```

   次の行を追加:

   ```
   net.ipv4.ip_forward=1
   ```

## 🛑 ホットスポットの停止

ホットスポットを停止するには、以下を実行します。

```bash
nmcli connection down Hotspot
```
