---
title: BredOS 上で仮想マシンを実行する
description:
published: true
date: 2025-09-15T11:13:57.999Z
tags: vm, how-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 1. はじめに

このガイドでは、BredOS の `virt-manager` を使用して仮想マシンのセットアップと管理をお手伝いします。

# 2. 前提条件

始める前に、以下のことを確認してください。

- 動作中のインターネット接続
- `sudo` 特権

# 3. インストール

## 3.1 必要なパッケージのインストール

開始するには、 `qemu` と `virt-manager` に必要なパッケージをインストールする必要があります。

```
sudo pacman -Syu virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

> `qemu`はハイパーバイザーですが、`virt-manager`はGUIベースの管理ツールです。
> {.is-info}

## 3.2 Libvirt サービスの有効化と開始

- パッケージがインストールされたら、`libvirtd` サービスを有効にして起動します。

```bash
sudo systemctl enable --now libvirtd
```

- サービスが実行されていることを確認するには:

```bash
sudo systemctl status libvirtd
```

## 3.3 ユーザーを `libvirt` グループに追加します

- VMを管理するためのルート権限を必要としないようにするには、ユーザーを`libvirt`グループに追加してください。

```bash
sudo usermod -aG libvirt $(whoami)
```

> これにより、ユーザーレベルからVMを管理できます。 これは危険なことができます!
> {.is-warning}

- 自分自身をグループに追加した後、ログアウトして変更を反映させるためにログインし直します。

## 3.4 ネットワークの設定

- `virt-manager` はネットワーク管理に `dnsmasq` を使用します。 デフォルトのネットワーク設定で `libvirt` が設定されていることを確認してください。 `virt-manager` はネットワーク管理に `dnsmasq` を使用します。 デフォルトのネットワーク設定で `libvirt` が設定されていることを確認してください。 デフォルトのネットワーク設定で `libvirt` が設定されていることを確認してください。

```bash
sudo virsh net-start default
sudo virsh net-autostart default
```

## 3.5 Virt-Manager を起動

- すべてがセットアップされたので、`virt-manager`を開始できます。

```bash
virt-manager
```

- これにより、 `virt-manager` GUIが開き、仮想マシンの作成と管理ができます。
  ![virt.jpg](/vms/virt.jpg)

> ユーザーを `libvirt` グループに追加していない場合は、今すぐパスワードを入力する必要があります。
> {.is-info}

![virt.jpg](/vms/virt.jpg)

## 3.6 XML 編集を有効にする

- XML 編集を有効にするには、`virt-manager` を開き、 `Edit` そして `Preferences` と `Enable XML editing` に移動する必要があります。

![xmlediting.jpg](/vms/xmlediting.jpg)

## 3.7 仮想マシンを作成

- `virt-manager` を開きます。
  `virt-manager` を開きます。
  ![virt.jpg](/vms/virt.jpg)
  `virt-manager` を開きます。
  ![virt.jpg](/vms/virt.jpg)

`virt-manager` を開きます。
![virt.jpg](/vms/virt.jpg)

- アイコンをクリックすると、新しい仮想マシンの下のスクリーンショットに表示されるようになります。

![virtnewvm.jpg](/vms/virtnewvm.jpg)

- インストール元(ISOイメージまたはネットワークインストール)を選択します。
  ![newvm.jpg](/vms/newvm.jpg)

![newvm.jpg](/vms/newvm.jpg)

- ウィザードに従って、CPU、RAM、およびVMストレージを割り当てます。 ⚙️

> RK3588では、小さな大きなアーキテクチャにより、vmあたり最大4コアを割り当てることができます。
> {.is-warning}

![cpuram.jpg](/vms/cpuram.jpg)
![disk.jpg](/vms/disk.jpg)

- ほとんどとCPU上。 RK3588 のような ig アーキテクチャは、「インストールする前に設定をカスタマイズ」にチェックを入れ、cpuコアの割り当てを担当する xml を編集する必要があります。

![finalstep.jpg](/vms/finalstep.jpg)

- 「終了」をクリックします

![vcpuxml0.jpg](/vms/vcpuxml0.jpg)

- CPU構成を開き、XMLタブを開きます。

![vcpuxml1.jpg](/vms/vcpuxml1.jpg)

- `<vcpu>XYZ</vcpu>`を見つけて、次の場所に置き換えます:

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

- cpuセットは0-3を使用したいコアで、rk3588と4-7のEコアはパフォーマンスコアとコア数です。 上記の例では、vmは2つのコアを持ち、ダイ自体にコア別名コア1と2を持つことになります。

![vcpuxml2.jpg](/vms/vcpuxml2.jpg)

- 周辺機器のハードウェアとグラフィックスのサポートを追加します。 🖥️

- VM ページに戻り、「ハードウェアを追加」を押します。

![addhw.png](/vms/addhw.png)

- 表示されるウィンドウから「ビデオ」を選択し、モデル選択から「ramfb」を選択し、「終了」をクリックします。

![gpu.png](/vms/gpu.png)

- グラフィックサーバーを追加するには、再度「ハードウェアを追加」を選択し、「グラフィックス」をクリックします。

![graphics.png](/vms/graphics.png)

- キーボードとマウスの場合は、同じ手順を繰り返してください。
  `Input` -> `USB Keyboard` と `Input` -> `EvTouch USB Graphics Tablet`

![tab.png](/vms/kb.png)
![tab.png](/vms/tab.png)

- 設定が完了したら、VM を起動します。 🟢

![startvm.jpg](/vms/startvm.jpg)

> これがあります Bred内でBredを実行できるようになりました！
> {.is-success}

## 3.8 追加設定

- コマンドラインでVMを管理するには、`virsh`を使用します。

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

## 3.9 トラブルシューティング

- **権限の問題**: ユーザーが `libvirt` グループにいることと、 `libvirtd` サービスが実行されていることを確認してください。
- **ネットワーク上の問題**: VM がインターネットにアクセスできない場合は、デフォルトの `virsh` ネットワークが実行されていることを確認してください。

