---
title: BredOS でデスクトップ環境を切り替える
description: BredOS 上で GNOME デスクトップ環境にインストールして切り替える方法を学びます。
published: true
date: 2025-09-18T07:46:58.501Z
tags: カスタマイズ
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 1. BredOS 上の GNOME Desktop

## 1.1 Install Gnome

GNOME デスクトップ環境はパッケージ `gnome` でインストールできます。\
インストールするには、以下を実行してください。

- インストールするには、以下を実行してください。

```
pacman -S gnome
```

GNOMEエコシステムを拡張した様々な追加のアプリケーションを含む`gnome-circle`と、開発ツールを含む`gnome-extra`、さらにGNOMEに適合するいくつかのアプリケーションやゲームをインストールすることができます。

## 1.2 GDMに切り替える

適切な操作を行うには、インストール後に **GDM** に切り替える必要があります。\
次のコマンドを実行します。

- 次のコマンドを実行します。

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

> Wayland の GNOME のみがサポートされています。
> {.is-warning}
> {.is-warning}

## 1.3 画面回転の修正

**画面が間違って回転している場合**画面回転\*\*拡張機能をインストールして設定できます。

### 1.3.1 拡張機能マネージャのインストール

- 実行:

```
sudo pacman -S extension-manager
```

インストールが完了したら、アプリケーションを開きます。

### 1.3.2 インストール画面の回転

アプリケーション内:

- `ブラウズ` > `検索` をタップ
- 「画面の回転」と入力します
- **shyzus**によって`Screen Rotate`をインストールします。

### 1.3.3 画面回転の設定

- 拡張機能マネージャの「インストール済み」タブに移動します。
- ギアアイコンをタップすると、拡張機能の設定が開きます。
- "向きオフセットを設定" の値を `1` に増やします。

## 1.4 ランドスケープスタイラスの使用法

お使いのデバイスがスタイラスに対応している場合、デフォルトで画面が垂直方向に回転されている場合にのみ、正しくポイントされます。
代わりに水平方向に動作するように設定するには、次の手順に従います。

### 1.4.1 udev ルールを編集

- `fydetab.rules`ファイルを編集するには、以下を実行します。

```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 1.4.2 設定行の追加

- ファイルの一番下に以下を追加します。

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 0 1"
```

Ctrl + Sを押して保存し、Ctrl + Xを押して終了します。

# 2. BledOS 上のプラズマデスクトップ

## 2.1 Install KDE Plasma

Plasma デスクトップ環境は `plasma-desktop` パッケージでインストールできます。\
インストールするには、以下を実行してください。

- インストールするには、以下を実行してください。

```
pacman -S plasma-desktop
```

これは、プラズマデスクトップの最小限の設置につながるはずです。 これは、プラズマデスクトップの最小限の設置につながるはずです。 より完全なKDEをインストールするには、完全なものを取得するためにパッケージ「plasma」か「plasma-meta」のいずれかを選択します。 グループとメタ パッケージの違いを理解するには、 [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) をクリックします。
グループとメタ パッケージの違いを理解するには、 [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) をクリックします。

> このソフトウェアは廃止されているため、SDDMの使用を避けてください! LightDMはプラズマでうまく動作します。
> {.is-warning}
> {.is-warning}
