---
title: systemd-nspawn コンテナの管理
description:
published: false
date: 2025-09-25T10:54:42.662Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🔄 1. 入門情報

`systemd-nspawn` は、コマンドやOS環境を厳密に隔離された環境で実行するように設計された軽量のコンテナツールです。 多くの場合、「ステロイドのクロート」として記述されています。 Linux ディストリビューション全体または最小限の環境を安全かつ制御された方法でテストまたは実行するための便利な方法を提供します。

QEMUやDockerのようなコンテナプラットフォームのような完全な仮想化ソリューションとは異なり、`systemd-nspawn`はLinux名前空間とcgroupsを使用してオーバーヘッドがほとんどないコンテナを作成します。

# 3. コンテナーテンプレートを作成

nspawn を使用するコンテナはファイルシステム上の任意の場所から実行できますが、推奨フォルダは `/var/lib/machines` です。 このフォルダの中に、Linux/GNU rootfsを保持するサブフォルダを作成します。 プロセスを簡単にするために、この記事ではコンテナテンプレートを作成する方法について説明します。 そのテンプレートフォルダの内容を新しい場所にコピーし、新しいコンテナ環境として使用することができます。

- ルートユーザーに切り替える:

```
sudo su
```

- 次に、ディレクトリを `/var/lib/machines`に変更します。

```
cd /var/lib/mains
```

- テンプレートフォルダを作成します。

```
mkdir テンプレート
```

コンテナはどのディストリビューションのルートをもつことができるので、あなたは比較的自由に選択できます。 Debian、Ubuntu、BredOSなど、最小限のディストリビューションのtarballのリストを提供します。 ただし、この記事は特にブレッドOSコンテナ用であることに注意してください。

> コンテナー内で実行する必要があるコマンドは、BredOS を使用していない場合は、ディストリビューションのバリアントに従って調整する必要があります。
> {.is-warning}

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) 選択肢のリリースを調べて、CPU アーキテクチャの `.tar.gz` をダウンロードします。
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) 下にスクロールしてダウンロードしたいリリースをクリックし、CPU アーキテクチャの `.tar.gz` をダウンロードします。
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) スクロールして、 `Container Base` または `Container Minimal Base` を選択します。
- [Arch Linux](https://archlinux.org/download/) 近くのミラーを選択し、`.tar.zst` ファイルをダウンロードします。
- [Arch Linux ARM](https://archlinuxarm.org/os/) `latest`と`aarch64`または`armv7`タグの.tar.gzファイルをダウンロードします。
  {.links-list}

> BredOS のrootfsがすぐに利用可能になります!
> これを実行することはできません！
> {.is-warning}
> {.is-warning}

選択した rootfs tarball をダウンロードした後、抽出する必要があります。 この例では、Arch Linux ARM tarballをダウンロードし、BredOSに変換しました。

- tarball を `/var/lib/machines/template` に展開します。

```
tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- `template` フォルダの内容は次のようになります。

```
ls template/
bin boot dev etc home lib mnt opt proc root run sbin srv syss tmp usr var
```

- コンテナを入力するには、以下を実行します。

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template
```

パラメータ `--machine` はコンテナの名前を定義し、`--directory` はコンテナの場所を指す。 コンテナを終了するには <kbd>Ctrl</kbd> + <kbd>D</kbd> または <kbd>Ctrl</kbd> + <kbd>]</kbd> を 1 秒以内に 3 回入力します。

コンテナ内で最初にしたいことは、パッケージマネージャーを初期化してシステムを更新することです。

- これを行うには、次を実行します。

```
pacman-key --init
pacman-key --populate
pacman -Syu
```

> ホスト名の解決に問題が発生した場合は、ホストシステムから `/var/lib/machines/template/etc/resolv.conf` ファイルを削除してください。
> {.is-warning}

- その後、カーネルやファームウェアのような不要なものを削除する必要があります。

```
pacman -R linux-aarch64 linux-firmware
```

- コンテナーを BredOS に変換するには、以下を実行します。

```
pacman-key --recv-keys 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
pacman-key --lsign-key 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
echo -e '# --> BredOS Mirrorlist <-- #\n\n# BredOS Main mirror\nServer = https://repo.bredos.org/repo/$repo/$arch\n' | tee /etc/pacman.d/bredos-mirrorlist
```

- ミラーファイルを編集します:

```
nano /etc/pacman.conf
```

- ファイルの最後に以下を追加します。

```
[BredOS-any]
Include = /etc/pacman.d/bredos-mirrorlist

[BredOS]
Include = /etc/pacman.d/bredos-mirrorlist
```

<kbd>Ctrl</kbd> + <kbd>X</kbd> と <kbd>Y</kbd>

- 最後に変換を開始します:

```
pacman -Syu bred-os-release BredOS-any/lsb-release bredos-logo
```

- 必要に応じて、bredos-config や bredos-news をインストールします。

```
pacman -Sy bredos-config bredos-news
```

# 4. 仮想ネットワークを使用してコンテナを実行

セクションで作成したコンテナ [2. コンテナーテンプレートを作成](#h-3-create-container-template) ホストシステムのネットワークを使用しました。 コンテナ上で仮想ネットワークデバイスを使用する場合、例えば[Open vSwitch](/how-to/open-vswitch)を使用する場合は、以下の手順を実行します。

- 新しいコンテナでこれを行いたい場合は、以下のようにします。

```
mkdir /var/lib/machines/template-veth
rsync -avP /var/lib/machines/template/* /var/lib/machines/template-veth/
```

> このガイドを簡単にするために、format@@0で作成したテンプレートを使い続けます。 コンテナテンプレートを作成](#h-3-create-container-template ) 。
> {.is-warning}

- 最初に、以前のようにコンテナを入力します:

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template
```

systemdのテーマを維持するために、 `systemd-networkd` を使用して仮想ネットワークデバイスを設定します。

- 次の2つの構成ファイルを作成します:

```
touch /etc/systemd/network/80-container-host0.network
nano /etc/systemd/network/99-wolVeth.network
```

- 以下を設定ファイルに貼り付けます:

```
[Match]
Name=host0

[Network]
Address=<containers ip address> example -> 192.168.1.100/24
Gateway=<gateway of that network> example -> 192.168.1.1
DNS=<DNS Servers address> example -> 9.9.9.9
#DHCP=yes -> or comment Address, Gateway and DNS and uncomment DHCP to assign the address automatically
```

- 最後に、`systemd-networkd`を有効にします。

```
systemctl enable systemd-networkd
```

コンテナがそのサービスを開始させるには、起動する必要があります (前のコマンドは chrootのようなものです)。 `--boot` パラメータを使用してこれを達成します。 さらに、`--network` パラメータを追加して、仮想ネットワークデバイスでコンテナを起動します。

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template --boot -network
```

これでコンテナを起動し、ログインプロンプトが表示されます。 root としてログインすることはできませんので、コンテナを起動する前にユーザを作成するか、セクションに進んでください[4. コンテナをサービスとして実行する](#h-4-run-container-as-a-service)。

- ユーザーを作成するには、コンテナ内で以下を実行します。

```
useradd <your username here>
passwd <your username here>
```

> 仮想ネットワークデバイスを実際のネットワークに使用したい場合は、さらなる設定が必要になります。 Use, for example, [Open vSwitch](/how-to/open-vswitch) or a simple bridge device to connect the virtual network device to something.
> {.is-warning}

# 🚀 4. コンテナをサービスとして実行

コンテナをサービスとして起動することも可能です。例えば、ブート時に起動することも可能です。 systemd-nspawn@.service ユニットを通じて実装がありますが、それを設定するためにオーバーライドファイルを作成する必要があります。 私たちの好ましい方法は、コンテナに使用したいすべてのパラメータを含む新しいservicefileを作成することです。

- 新しいコンテナを作成するためにテンプレートをクローンします:

```
mkdir /var/lib/machines/my-first-container
rsync -avP /var/lib/machines/template/* /var/lib/machines/my-first-container/
```

- 次に、ホストに新しいサービスファイルを作成します。

```
sudo nano /etc/systemd/system/<your containers name here>.service
```

- 次の内容に貼り付けてください：

```
[Unit]
Description=<your containers name here>
After=network.target
Requires=network.target

[Service]
ExecStart=/usr/bin/systemd-nspawn --machine=<your containers name here> --directory=/var/lib/machines/my-first-container --boot
KillMode=mixed
Type=notify
Restart=always

[Install]
WantedBy=multi-user.target

```

コンテナ上で仮想ネットワークデバイスを使用したい場合は、 `ExecStart=/usr/...` の末尾に `--network` を追加します。

- その後、次のようにコンテナを起動できます。

```
sudo systemctl start <your containers name here>.service
```

- または、起動時に起動させてください:

```
sudo systemctl enable <your containers name here>.service
```

- コンテナにログインするには、 `machinectl` を使用します。

```
sudo machinectl shell <your containers name here>
```

- 実行中のすべてのコンテナ (およびVM) を以下に確認します。

```
《須藤機械》
```

# 🔄 3. コンテナ内からホスト上のファイル/フォルダにアクセスする

名前が示すように、コンテナは通常、ホストシステムにアクセスできません。 これは、コンテナがホストシステム上の特定のファイルやフォルダにアクセスできるように変更することができます。 たとえば、追加のストレージスペースを提供したり、ご使用の GPU へのコンテナアクセスを許可するなどです。

- `--bind`パラメータでファイル/フォルダへのアクセスを行うことができます。

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template --bind=<path to your location>
```

- たとえば、自宅のフロアを共有したい場合:

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template --bind=/home
```

フォルダ`/home`をコンテナ内の同じ場所にマウントします。 コンテナ内のマウントポイントを変更したい場合は、両方のパス間で <kbd>:</kbd> を使用して指定できます。

- 例えば、 `/tmp/home`を`/tmp/home`にしたい場合:

```
systemd-nspawn --machine="テンプレート" --directory=/var/lib/machines/template --bind=/home:/tmp/home
```

# 8. 追加メモ

`systemd-nspawn` は非常に強力なツールです。 ここで私たちが取り上げたのは、基本的なことです。 驚かせたいなら、彼らの [man page](https://www.freedesktop.org/software/systemd/man/latest/systemd-nspawn.html) を見てみよう！