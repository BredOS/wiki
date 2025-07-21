---
title: FydetabのGNOME
description:
published: true
date: 2024-11-12T15:33:19.071Z
tags:
editor: markdown
dateCreated: 2024-11-10T19:41:06.111Z
---

# Fydetab Duo上のGNOMEデスクトップ

gnome-desktop は AUR パッケージ `gnome-meta` でインストールできます。
`yay -S gnome-meta` でインストールします。

---

適切な操作を行うには、インストール時に GDM に切り替える必要があります。 以下の手順で実行できます。

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

Gnomeのウェイランドだけが全くサポートされています。

## 画面の回転を修正

Fydetabの画面が正しく回転しない場合は、拡張機能「Screen Rotate」をインストールして設定する必要があります。

### 1. 拡張機能マネージャのインストール

`sudo pacman -S extension-manager` を実行してインストールし、アプリケーションを開きます。

### 2. 画面の回転をインストール

アプリを開いたら、`Browse` > `Search` > `Screen rotate` と入力します。

### 3. 画面回転の設定

拡張機能マネージャの「インストール済み」ページに戻り、設定の歯車をタップして拡張機能の設定パネルを開きます。
そして、`向きをオフセットにする` の値を 1 に増やします。

## ランドスケープスタイラスペンの使用状況

スタイラスはデフォルトで画面が垂直方向に回転している場合にのみ正しくポイントされます。
これを水平方向に動作させるには:

### 1. `/etc/udev/rules.d/fydetab.rules` を開く

ファイルを開くには、以下を実行します。

```
sudo nano /etc/udev/rules.d/fydetab.rules
```

### 2. 設定行を追加

ファイルの一番下に以下を追加します。

```
SUBSYSTEM=="input", ENV{ID_INPUT_TABLET}=="1", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 0 1"
```

Ctrl + Sを押して保存し、Ctrl + Xを押して終了します。

### 3. Reboot

再起動後、ペンは正常に動作します。

誤ってGNOME設定のスタイラス校正を試した場合は、以下を実行してキャリブレーションデータを削除してください。

```
dconf reset -f /org/gnome/desktop/pakts
```