---
title: BredOS でデスクトップ環境を切り替える
description: BredOS 上で GNOME デスクトップ環境にインストールして切り替える方法を学びます。
published: true
date: 2025-09-13T10:07:12.684Z
tags: カスタマイズ
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 1. Gnome

## 🎨 1.1. BredOS 上の GNOME Desktop

GNOME デスクトップ環境はパッケージ `gnome` でインストールできます。\
インストールするには、以下を実行してください。

```
pacman -S gnome
```

GNOMEエコシステムを拡張した様々な追加のアプリケーションを含む`gnome-circle`と、開発ツールを含む`gnome-extra`、さらにGNOMEに適合するいくつかのアプリケーションやゲームをインストールすることができます。

---

## 🔄 1.2. GDMに切り替える

適切な操作を行うには、インストール後に **GDM** に切り替える必要があります。\
次のコマンドを実行します。\
次のコマンドを実行します。

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

📝 **Note:** Wayland の GNOME のみがサポートされています。

---

## 🔄 🖥️ 1.3. 画面回転の修正

**画面が間違って回転している場合**画面回転\*\*拡張機能をインストールして設定できます。

### 1️⃣ 1.3.1 拡張機能マネージャのインストール

実行:

```
sudo pacman -S extension-manager
```

インストールが完了したら、アプリケーションを開きます。

### 2️⃣ 1.3.2 インストール画面の回転

アプリケーション内:

- `ブラウズ` > `検索` をタップ
- **画面の回転** と入力します
- **shyzus**によって`Screen Rotate`をインストールします。

### 3️⃣ 1.3.3 画面回転の設定

- 拡張機能マネージャの「インストール済み」タブに移動します。
- ⚙️アイコンをタップして拡張機能の設定を開きます。
- **向きオフセットを設定**の値を`1`に増やします。

---

> ✅ 完了！ ✅ 完了！ GNOME は BredOS 上で適切に設定されました。 🚀 🚀\
> {.is-success}

# 2. KDE Plasma

## 🎨 2.1. BledOS 上のプラズマデスクトップ

Plasma デスクトップ環境は `plasma-desktop` パッケージでインストールできます。\
インストールするには、以下を実行してください。

```
pacman -S plasma-desktop
```

これは、プラズマデスクトップの最小限の設置につながるはずです。 より完全なKDEをインストールするには、完全なものを取得するためにパッケージ「plasma」か「plasma-meta」のいずれかを選択します。 グループとメタ パッケージの違いを理解するには、 [here](https://wiki.archlinux.org/title/Meta_package_and_package_group) をクリックします。

> このソフトウェアは廃止されているため、SDDMの使用を避けてください! LightDMはプラズマでうまく動作します。
> {.is-warning}
