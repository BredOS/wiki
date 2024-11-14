---
title: BredOS 上で仮想マシンを実行する方法
description: null
published: true
date: 2024-11-14T19:23:33.286Z
tags: vm, how-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 🚀 Virt-Manager で BredOS 上で仮想マシンを実行する

このガイドでは、BredOS の `virt-manager` を使用して仮想マシンのセットアップと管理をお手伝いします。

## 📋 前提条件

始める前に、以下のことを確認してください。

- 動作中のインターネット接続 🌐
- Sudoの権限🔑

## ステップ1: 必要なパッケージのインストール 📦

まず、KVM と `virt-manager` に必要なパッケージをインストールする必要があります。

```bash
sudo pacman -Syu
sudo pacman -S virt-manager qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

## ステップ2：Libvirtサービスの有効化と開始 <unk>

パッケージがインストールされたら、`libvirtd` サービスを有効にして起動します。

```bash
sudo systemctl enable --now libvirtd
```

サービスが実行されていることを確認するには:

```bash
sudo systemctl status libvirtd
```

## ステップ 3: ユーザーを `libvirt` グループ :busts_in_siliette: に追加します。

VMを管理するためのルート権限を必要としないようにするには、ユーザーを`libvirt`グループに追加してください。

```bash
sudo usermod -aG libvirt $(whoami)
```

自分自身をグループに追加した後、ログアウトして変更を反映させるためにログインし直します。

## ステップ 4: ネットワーク設定 🌐

`virt-manager` はネットワーク管理に `dnsmasq` を使用します。 デフォルトのネットワーク設定で `libvirt` が設定されていることを確認してください。

```bash
sudo virsh net-start default
sudo virsh net-autostart default
```

## ステップ 5: Virt-Manager :desktop_computerを起動します:

すべてがセットアップされたので、`virt-manager`を開始できます。

```bash
virt-manager
```

これにより、 `virt-manager` GUIが開き、仮想マシンの作成と管理ができます。
![virt.jpg](/vms/virt.jpg)

## ステップ 6: XML 編集を有効にする

XML編集を有効にするには（後で必要）`virt-manager`を開く必要があります。**Edit**から**Preferences**に行き、XML編集
を有効にします。[xmlediting.jpg](/vms/xmlediting.jpg)

## ステップ 7: 仮想マシンを作成する 🛠️

1. `virt-manager` を開きます。
   ![virt.jpg](/vms/virt.jpg)
2. **新しい仮想マシンを作成** ➕をクリックしてください。
   ![virtnewvm.jpg](/vms/virtnewvm.jpg)
3. インストール元(ISOイメージまたはネットワークインストール)を選択します。
   ![newvm.jpg](/vms/newvm.jpg)
4. ウィザードに従って、CPU、RAM、およびVMストレージを割り当てます。 ⚙️

> RK3588では、小さなアーキテクチャ
> {.is-warning} により、vmあたり最大4コアを割り当てることができます。

![disk.jpg](/vms/disk.jpg)
![cpuram.jpg](/vms/cpuram.jpg)
5. On CPUs with the little.big architecture like the RK3588 you need to check "Customize configuration before install" and edit the xml responsible for allocating cpu cores
![finalstep.jpg](/vms/finalstep.jpg)
Click **Finish**
![vcpuxml0.jpg](/vms/vcpuxml0.jpg)
Open the **CPUs** configuration and then the **XML** tab
![vcpuxml1.jpg](/vms/vcpuxml1.jpg)
Locate `<vcpu>XYZ</vcpu>` and replace it with

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

cpuセットは0-3を使用したいコアで、rk3588と4-7のEコアはパフォーマンスコアとコア数です。 上記の例では、vmは2つのコアを持ち、ダイ自体にコア別名コア1と2を持つことになります。
![vcpuxml2.jpg](/vms/vcpuxml2.jpg)

5. 設定が完了したら、VM を起動します。 🟢

![startvm.jpg](/vms/startvm.jpg)

## 追加設定 ⚙️

- コマンドラインでVMを管理するには、`virsh`を使用します。

```bash
virsh list --all
virsh start <vm-name>
virsh shutdown <vm-name>
```

## :hammer_and_wrenchのトラブルシューティング:

- **権限の問題**: ユーザーが `libvirt` グループにいることと、 `libvirtd` サービスが実行されていることを確認してください。
- **ネットワーク上の問題**: VM がインターネットにアクセスできない場合は、デフォルトの `virsh` ネットワークが実行されていることを確認してください。

## 🎉 結論

BredOS で `virt-manager` のセットアップに成功し、仮想マシンの作成と管理の準備が整いました！
