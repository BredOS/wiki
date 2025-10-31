---
title: BredOS 上で仮想マシンを実行する方法
description:
published: true
date: 2025-09-17T10:43:46.119Z
tags: vm, how-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 1. はじめに

このガイドでは、BredOS の `virt-manager` を使用して仮想マシンのセットアップと管理をお手伝いします。

# 2. 📋 前提条件

始める前に、以下のことを確認してください。

- 動作中のインターネット接続 🌐
- `sudo` 特権

# 3. インストール

## 3.1 必要なパッケージのインストール

- まず、KVM と `virt-manager` に必要なパッケージをインストールする必要があります。

```
sudo pacman -Syu
sudo pacman -S virt-manager qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

> これにより、ユーザーレベルからVMを管理できます。 これは危険なことができます!
> {.is-warning}

## ステップ2：Libvirtサービスの有効化と開始 <unk>

- パッケージがインストールされたら、`libvirtd` サービスを有効にして起動します。

```bash
sudo systemctl enable --now libvirtd
```

- サービスが実行されていることを確認するには:

```bash
sudo systemctl status libvirtd
```

## ステップ 3: ユーザーを `libvirt` グループ 👥 に追加します。

- VMを管理するためのルート権限を必要としないようにするには、ユーザーを`libvirt`グループに追加してください。

```bash
sudo usermod -aG libvirt $(whoami)
```

> これにより、ユーザーレベルからVMを管理できます。 これは危険なことができます! これは危険なことができます!
> {.is-warning}

- 自分自身をグループに追加した後、ログアウトして変更を反映させるためにログインし直します。

## ステップ 4: ネットワーク設定 🌐

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

![startvm.jpg](/vms/startvm.jpg)

> ユーザーを `libvirt` グループに追加していない場合は、今すぐパスワードを入力する必要があります。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

## ステップ 6: XML 編集を有効にする

- XML編集を有効にするには（後で必要）`virt-manager`を開く必要があります。**Edit**から**Preferences**に行き、XML編集
  を有効にします。[xmlediting.jpg](/vms/xmlediting.jpg)

# 4. 3.7 仮想マシンを作成

- アイコンをクリックすると、新しい仮想マシンの下のスクリーンショットに表示されるようになります。

- インストール元を選択します(ローカルメディアまたはネットワークインストール)。

- ローカル インストール メディアを選択した場合は、ウィザードを使用して .iso ファイルを選択します。

- ウィザードに従って、CPU、RAM、およびVMストレージを割り当てます。 ⚙️

> これにより、ユーザーレベルからVMを管理できます。 これは危険なことができます!
> {.is-warning}

- ほとんどとCPU上。 RK3588 のような ig アーキテクチャは、「インストールする前に設定をカスタマイズ」にチェックを入れ、cpuコアの割り当てを担当する xml を編集する必要があります。

- 「終了」をクリックします

新しいウィンドウが開き、仮想マシンを作成する前に設定を編集できます。 CPU構成を開き、次にXMLタブを開きます。 新しいウィンドウが開き、仮想マシンを作成する前に設定を編集できます。 CPU構成を開き、次にXMLタブを開きます。 CPU構成を開き、XMLタブを開きます。

- `<vcpu>XYZ</vcpu>`を見つけて、次の場所に置き換えます:

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

> `cpuセット`がある場合、使用するコアはRK3588の0-3(Eコア)、パフォーマンスコアの場合は4-7です。
> 上記の例では、VMは効率コア(ダイ自体のコア1と2)である2つのコアを持っています。
> {.is-info}
> 上記の例では、VMは効率コア(ダイ自体のコア1と2)である2つのコアを持っています。
> {.is-info}

- 設定が完了したら、VM を起動します。 🟢

> これがあります Bred内でBredを実行できるようになりました！
> {.is-success}

# 5. 3.8 追加設定

- コマンドラインでVMを管理するには、`virsh`を使用します。

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```


