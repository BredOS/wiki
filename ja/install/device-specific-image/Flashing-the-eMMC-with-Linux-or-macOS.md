---
title: Linux または macOS で eMMC の書き込み
description:
published: true
date: 2025-10-05T06:59:09.446Z
tags:
editor: markdown
dateCreated: 2025-09-16T06:29:26.865Z
---

# 1. はじめに

このガイドでは、ツール `rkdeveloptool` を使用して eMMC をフラッシュする方法について説明します。 ほとんどのLinuxリポジトリで見つけることができ、macOS上でも動作します。 ほとんどのLinuxリポジトリで見つけることができ、macOS上でも動作します。 ほとんどのLinuxリポジトリで見つけることができ、macOS上でも動作します。

BredOS のインストールには、以下の3つのことが必要です。

1. SPL ローダーファイル:

### Tabset {.tabset}

#### RK3588

[`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)

#### RK3566

[`rk356x_spl_loader_ddr1056_v1.10.111.bin`](https://dl.radxa.com/rock3/images/loader/rock-3a/rk356x_spl_loader_ddr1056_v1.10.111.bin)

###

2. Device Specific Image from our [official website](https://bredos.org/download.html)
3. `rkdeveloptool`

> 画像は .xz 圧縮ファイルとして提供します。 画像は .xz 圧縮ファイルとして提供します。 書き込みの前に含まれている .img ファイルを抽出する必要があります。
> {.is-warning}
> これを実行することはできません！
> {.is-warning}
> {.is-warning}

# 3. フラッシュ中

`rkdeveloptool` のインストールは以下の手順で行うことができます。

## 2.1 Linux

- Archベースのディストリビューションを使用している場合

```
sudo pacman -S rkdeveloptool-git
```

- Debian ベースのディストリビューションを使用している場合

```
sudo apt install rkdeveloptools
```

- Red Hat ベースのディストリビューションを使用している場合

```
sudo dnf install rkdeveloptool
```

## 2.2 macOS

### 2.2.1 前提条件

macOS用の`rkdeveloptool`のバイナリパッケージがないので、自分でコンパイルする必要があります。 そのためには、 [Brew](https://brew.sh/) 経由でパッケージをインストールする必要があります。 そのためには、 [Brew](https://brew.sh/) 経由でパッケージをインストールする必要があります。 そのためには、 [Brew](https://brew.sh/) 経由でパッケージをインストールする必要があります。

- 次のコマンドで`automake`、`autoconf`、`libusb`、`pkg-config`、`git`、`wget`をインストールします。

```
brew install automake autoconf libusb pkg-config git wget
```

### 2.2.2 リポジトリを複製

- 以下のソースコードを入手してください。

```
git clone https://github.com/rockchip-linux/rkdeveloptool
```

### 2.2.3 バイナリにコンパイルする

- ソースコードが含まれるディレクトリに変更し、それを補完します。

```
cd rkdeveloptool
autoconf -i
./configure
make -j $(nproc)
```

- `make`プロセスがエラーなく終了したら、現在のフォルダ内に`rkdeveloptool`ファイルがあります。

```
ls | grep rkdeveloptool
```

- 出力すべきです

```
rkdeveloptool
```

### 2.2.4 実行させる

- 最後に、`opt`フォルダにコピーして、どこからでも実行できます。

```
cp rkdeveloptool /opt/homebrew/bin/
```

# 3. フラッシュ中

## 3.1 マスクロームを入力

USB経由でフラッシュ可能なデバイスとしてSBCを表示するには、`maskromモード`に設定する必要があります。 これは、使用しているデバイスによって異なります。 一部のSBCにはボタンがありますが、または2つのピンを短くする必要があります。 SBCメーカーのマニュアルを参照してください。 これは、使用しているデバイスによって異なります。 一部のSBCにはボタンがありますが、または2つのピンを短くする必要があります。 SBCメーカーのマニュアルを参照してください。 これは、使用しているデバイスによって異なります。 一部のSBCにはボタンがありますが、または2つのピンを短くする必要があります。 SBCメーカーのマニュアルを参照してください。

- この情報は Google 検索で簡単に見つけることができます:

```
マスクロームモード <your sbcs name here>
```

- お使いのデバイスが`maskromモード`であり、PCの実行によって正しく検出されたことを確認するには、次のようにします。

```
sudo rkdeveloptool ld
```

- 以下が表示された場合は、移動するのが良いです(出力は似ていますが、同一ではありません):

```
DevNo=1 Vid=0x2207,Pid=0x350b,LocationID=801マスク
```

> 電源が差し込まれている間、Maskromボタンを押したままにします。
> {.is-warning}

> USB-CからCへのケーブル、またはUSB-CからAへのケーブルを使用すると、ボードが検出されない可能性があります。
> USB-CをAケーブルに使用することをお勧めします。 次に、[USB-C メスから USB-A 男性アダプタ](https://www.aliexpress.com/item/1005004767752226.html)またはUSB-A ケーブル。
> これを実行することはできません！
> {.is-warning}
> {.is-warning}

## 3.2 フラッシュブレッドOS

これで `rkdeveloptool` を使ってデバイスにコマンドを送信できるようになったので、BredOS SBCを作ることができます。

- SPIローダーファイルをSBCに送信:

```
sudo rkdeveloptool db <path to SPI loader file here>
```

- 次に、BredOS デバイス固有のイメージを eMMC に書き込みます。

```
sudo rkdeveloptool wl 0 <path to BredOS image here>
```

- そして最後にデバイスを再起動します:

```
sudo rkdeveloptool rd
```

> フラッシュに成功したら[**最初のセットアップ**](/en/install/first-setup)で続行します。
> {.is-success}
> {.is-success}
> {.is-success}

# 🚀 4. 追加情報

人生でもっとプログレスバーが欲しいだけですよね？ 私たちはあなたをカバーし、心配しないでください。

## 4.1 選択したフラッシュメディア情報を読み込み中

`sudo rkdeveloptool rfi`コマンドは、選択したフラッシュメディアの詳細を表示します。

- デフォルトでは、これは通常、利用できない場合を除き、eMMCです。

```
Flash Info:
	Manufacturer: SAMSUNG, value=00
	Flash Size: 14910 MB
	Flash Size: 30535680 Sectors
	Block Size: 512 KB
	Page Size: 2 KB
	ECC Bits: 0
	Access Time: 40
	Flash CS: Flash<0>
```

## 4.2 フラッシュターゲットの変更

フラッシュ/ないeMMCではなく別のことをダンプしたいですか?

- SDカードを選択するには `sudo rkdeveloptool cs 2` 。
- `sudo rkdeveloptool cs 9` で SPINOR チップを選択します。
- `sudo rkdeveloptool cs 1` で再びeMMCを選択します。

変更は `sudo rkdeveloptool rfi` に反映されます。