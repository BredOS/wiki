---
title: systemd-nspawn でコンテナを管理
description:
published: false
date: 2025-09-25T07:02:39.910Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 🔄 1. 入門情報

`systemd-nspawn` は、コマンドやOS環境を厳密に隔離された環境で実行するように設計された軽量のコンテナツールです。 多くの場合、「ステロイドのクロート」として記述されています。 Linux ディストリビューション全体または最小限の環境を安全かつ制御された方法でテストまたは実行するための便利な方法を提供します。

QEMUやDockerのようなコンテナプラットフォームのような完全な仮想化ソリューションとは異なり、`systemd-nspawn`はLinux名前空間とcgroupsを使用してオーバーヘッドがほとんどないコンテナを作成します。

# 3. コンテナーテンプレートを作成

nspawn を使用するコンテナはファイルシステム上の任意の場所から実行できますが、推奨フォルダは `/var/lib/machines` です。 このフォルダの中に、Linux/GNU rootfsを保持するサブフォルダを作成します。 プロセスを簡単にするために、この記事ではコンテナテンプレートを作成する方法について説明します。 そのテンプレートフォルダの内容を新しい場所にコピーし、新しいコンテナ環境として使用することができます。

- ルートに切り替える:

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

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) 選択肢のリリースを調べて、CPU アーキテクチャ用の .tar.gz をダウンロードします。
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) 下にスクロールしてダウンロードしたいリリースをクリックし、CPU アーキテクチャ用の .tar.gz をダウンロードします。
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) 下にスクロールし、Container BaseまたはContainer Minimal Baseを選択します。
- [Arch Linux](https://archlinux.org/download/) Choose a mirror near you, then download the .tar.zst file.
- [Arch Linux ARM](https://archlinuxarm.org/os/) aarch64 または armv7 タグの .tar.gz ファイルをダウンロードします。
  {.links-list}

選択した rootfs ターボールをダウンロードしたら、それを抽出する必要があります。 この例では、Arch Linux ARM tarball をダウンロードし、あとで BredOS に変換します。

- tarball を `/var/lib/machines/template` に展開します。

```
sudo tar -xzf <your distro's tarball of choice> -C /var/lib/machines/template
```

- `template` フォルダの内容は次のようになります。

```
ls template/
bin boot dev etc home lib mnt opt proc root run sbin srv syss tmp usr var
```

