---
title: 仮想スイッチの管理方法
description:
published: true
date: 2025-09-24T12:11:02.185Z
tags:
editor: markdown
dateCreated: 2025-09-24T11:30:44.331Z
---

# 🔄 1. 入門情報

Open vSwitch (OVS) は、標準管理インターフェイスとプロトコルをサポートしながら、高度なネットワーク自動化を可能にするように設計されたオープンソースの多層仮想スイッチです。 仮想環境で主に使用され、仮想マシン(VM)間の通信やVMと物理ネットワーク間の通信を容易にします。 仮想環境で主に使用され、仮想マシン(VM)間の通信やVMと物理ネットワーク間の通信を容易にします。

# 📥 2. インストール

- OVSは、このコマンドを実行することでインストールできます。

```
sudo pacman -S openvswitch
```

- インストールが成功したら、OVSサービスを有効にして開始する必要があります。

```
sudo systemctl enable --now ovs-vswitchd
```

# 4. vSwitchを作成

OVSとそのスイッチは `ovs-vsctl` ツールで管理できます。

- 新しいスイッチを作成するには:

```
sudo ovs-vsctl add-br <your switch name here>
```

`<your switch name here>`をお好みの名前に置き換えてください。

# 🚀 4. 仮想ネットワークデバイスを接続する

## 4.1 手動で

仮想ネットワークデバイスは、ハイパーバイザを介して、またはコンテナを介して手動で作成できます。 彼らは表示され、物理的なネットワークデバイスのように機能します。 彼らは表示され、物理的なネットワークデバイスのように機能します。

- すべてのネットワークデバイスを一覧表示するには:

```
ip a
```

- 以下の出力例では、3つのデバイスが表示されます。

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp49s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master ovs-system state UP group default qlen 1000
    link/ether 00:48:54:20:41:e0 brd ff:ff:ff:ff:ff:ff
    altname enx0048542041e0
    inet6 fe80::248:54ff:fe20:41e0/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
3: ve-databaselCjq@if2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master ovs-system state UP group default qlen 1000
    link/ether 82:22:48:3a:2b:1a brd ff:ff:ff:ff:ff:ff link-netnsid 4
    altname ve-databaseserver.dmz
    inet 169.254.19.70/16 metric 2048 brd 169.254.255.255 scope link ve-databaselCjq
       valid_lft forever preferred_lft forever
    inet 192.168.244.177/28 brd 192.168.244.191 scope global ve-databaselCjq
       valid_lft forever preferred_lft forever
```

この例では、systemd-nspawn コンテナから生成された仮想ネットワークデバイスである `ve-databaselCjq` を使用します。

- vswitchに接続するには、以下を実行してください。

```
sudo ovs-vsctl add-port <your switch name here> ve-databaselCjq
```

- そのアダプターのパケットを特定の vlan にタグ付けしたい場合は、`tag` パラメータを使用します。

```
sudo ovs-vsctl add-port <your switch name here> ve-databaselCjq tag=<your vlan id tag here>
```

## 4.1 libvirt を介して自動的に

If you followed [this guide](/how-to/run-vms) to create the hypervisor stack with qemu/libvirt, you can add your newly created switch to the networks known by libvirt. これにより、GUIでvSwitchを選択することができ、VMの仮想ネットワークデバイスは起動時に自動的にそのvSwitchに追加されます。

- `virt-manager`を起動し、下のスクリーンショットで青とマークされている`QEMU/KVM`を右クリックします。 `Details` をクリックします。 `Details` をクリックします。

![main.png](/vswitch/main.png)

新しいウィンドウで、Tab `仮想ネットワーク`に切り替えて、左端の <kbd>+</kbd> サインをクリックします。

- 次に、`XML`タブに切り替えて、以下の内容を置き換えます:

```
<network>
  <name><your switch name here></name>
  <forward mode='bridge'/>
  <bridge name='<your switch name here>'/>
  <virtualport type='openvswitch'/>
  <portgroup name='vlan-01' default='yes'>
  </portgroup>
  <portgroup name='vlan-02'>
    <vlan>
      <tag id='2'/>
    </vlan>
  </portgroup>
</network>
```

- 指定された設定で`<your switch name here>`を2回置き換えます。 指定された設定で`<your switch name here>`を2回置き換えます。 `portgroup`-tag を使用すると、そのスイッチで使用する vlan を定義できます。

![network.png](/vswitch/network.png)

# 🔄 3. 物理ネットワークにvSwitchを接続

物理ネットワークにvSwitchを接続したい場合は、物理ネットワークデバイスを使用する必要があります。

> 使用するネットワークデバイスにはIPアドレスが割り当てられていない必要があります。
> {.is-warning}
> {.is-warning}

- 上記の出力例から `enp49s0` を追加するには、以下を実行します。

```
sudo ovs-vsctl add-port <your switch name here> enp49s0
```

物理的なネットワークデバイスが1つしかない場合、および/またはホストデバイスのネットワーク接続に使用したい場合。 物理ネットワークデバイスの代わりに、vSwitchにIPアドレスを割り当てる必要があります。 これは、たとえばネットワークマネージャの GUI やシステムを介して、任意のツールを使用して行うことができます。 これは、たとえばネットワークマネージャの GUI やシステムを介して、任意のツールを使用して行うことができます。

# 8. 2つのvSwitchesをインターネット上で接続する

インターネット経由でVPN経由で2つのデバイスを接続している場合は、vSwitchesを接続することができます。 これにより、これらのvSwitches上のデバイスは、さらなる設定なしに互いに通信できます。 vSwitchが物理スイッチに接続されている場合、インターネット経由で物理デバイスを接続することも可能です。 これは多くの目的のために有用である場合もある。 これにより、これらのvSwitches上のデバイスは、さらなる設定なしに互いに通信できます。 vSwitchが物理スイッチに接続されている場合、インターネット経由で物理デバイスを接続することも可能です。 これは多くの目的のために有用である場合もある。

- 両方のホストで以下を実行します:

```
sudo ovs-vsctl add-port <your switch name here> vxlan0 -- インターフェイス vxlan0 type=vxlan options:remote_ip=<IP address of other host>
```

As always, replace `<your switch name here>` with the name of your switch, and `<IP address of other host>` with the IP address of the host with the other vSwitch. これにより、接続されたデバイスはインターネット上で安全に通信できるようになりました。

> クライアントがお互いにpingできますが、さらなる通信が機能しない場合は、おそらくMTUの問題です。
> {.is-danger}
> {.is-danger}

## 6.1 MTUの問題を修正

MTUは、転送される各パケットの最大サイズを定義します。 通常、ping パケットはこの最大値まで満たされませんが、「本当の」通信は行います。 MTUは、転送される各パケットの最大サイズを定義します。 通常、ping パケットはこの最大値まで満たされませんが、「本当の」通信は行います。 デフォルトのMTUは1500バイトです。 トンネルを通してその大きさのパケットを送る場合トンネル自体は 送信元アドレスや宛先アドレスのような情報を追加する必要があります これは、MTUを超えてパケットが分割される可能性があり、クライアントの通信に問題が生じる可能性があります。 これを修正するには、例えば1200バイトのMTUを下げるだけです。 この調整は、DHCPサーバーまたは手動で行うことができます。 これは、MTUを超えてパケットが分割される可能性があり、クライアントの通信に問題が生じる可能性があります。 これを修正するには、例えば1200バイトのMTUを下げるだけです。 この調整は、DHCPサーバーまたは手動で行うことができます。

# 8. 追加コマンド

- vSwitchに接続されているすべてのデバイスを一覧表示するには、次を実行します。

```
sudo ovs-vsctl list-ports <your switch name here> 
```

- ネットワークデバイスを切断するには、以下を実行してください。

```
sudo ovs-vsctl del-port <your switch name here> <your adapters name here>
```

