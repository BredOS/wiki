---
title: ワイヤレスホットスポットとしてデバイスを使用する方法
description:
published: true
date: 2025-09-15T10:34:19.987Z
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

- 出力例
  ```
  DEVICE           TYPE      STATE                   CONNECTION      
  bridge0          bridge    connected               bridge0         
  tailscale0       tun       connected (externally)  tailscale0      
  lo               loopback  connected (externally)  lo              
  br-8a9f1336b961  bridge    connected (externally)  br-8a9f1336b961 
  br-aeeaf62e2336  bridge    connected (externally)  br-aeeaf62e2336 
  docker0          bridge    connected (externally)  docker0         
  virbr0           bridge    connected (externally)  virbr0          
  enp8s0           ethernet  connected (externally)  enp8s0          
  wlan0            wifi      disconnected            --   
  ```

- 次のコマンドを使用してホットスポットを作成します。

  ```bash
  nmcli デバイス wifi hotspot ifname <wifi_interface> ssid <MyHotspot> パスワード <mypassword>
  ```

- 出力例
  ```
  デバイス 'wlan0' successfully activated wd090d70-fd85-45bc-bf36-a63846f3f805' 
  ヒント: "nmcli dev wifi show-password" にはWi-Fi名とパスワードが表示されます。
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

- 出力例

```
NAME                            UUID                                  TYPE       DEVICE          
Hotspot                         4d090d70-fd85-45bc-bf36-a63846f3f805  wifi       wlan0           
bridge0                         210b2bd8-1a6b-43e6-9ed1-4abc50324505  bridge     bridge0         
tailscale0                      27e86e0c-a8c7-4374-9083-51454c4b8b3e  tun        tailscale0      
lo                              f6ba586b-a4c4-49c1-a0f3-3154f8eae92b  loopback   lo              
br-8a9f1336b961                 9a3d08b3-6516-4071-9369-30311a48b55a  bridge     br-8a9f1336b961 
br-aeeaf62e2336                 ee78e282-1516-45df-a6ec-cdcb9d989030  bridge     br-aeeaf62e2336 
docker0                         c5f70ee8-5407-4510-8b61-6fc0f15c2e81  bridge     docker0         
virbr0                          12d1109a-64a4-4d07-b0a2-887f10145109  bridge     virbr0          
enp8s0                          184c8145-ca17-4258-b7db-7e32c298f424  ethernet   enp8s0
```

アクティブな接続の下にホットスポットが表示されます (上の例では2行目)。

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
