---
title: BredOS で GNOME を使用するためにデスクトップ環境を切り替える
description: BredOS 上で GNOME デスクトップ環境にインストールして切り替える方法を学びます。
published: true
date: 2025-02-23T15:13:50.035Z
tags: カスタマイズ
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 🎨 BredOS 上の GNOME Desktop

GNOME デスクトップ環境は AUR パッケージ `gnome-meta` でインストールできます。\
インストールするには、以下を実行してください。

```
yay -S gnome-meta
```

---

## 🔄 GDM に切り替える

適切な操作を行うには、インストール後に **GDM** に切り替える必要があります。\
次のコマンドを実行します。

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

📝 **Note:** Wayland の GNOME のみがサポートされています。

---

## 🔄 🖥️ 画面の回転を修正

**画面が間違って回転している場合**画面回転\*\*拡張機能をインストールして設定できます。

### 1️⃣ 拡張機能マネージャのインストール

実行:

```
sudo pacman -S extension-manager
```

インストールが完了したら、アプリケーションを開きます。

### 2️⃣ 画面の回転

アプリケーション内:

- `ブラウズ` > `検索` をタップ
- **画面の回転** と入力します
- **shyzus**によって`Screen Rotate`をインストールします。

### 3️⃣ 画面の回転

- 拡張機能マネージャの「インストール済み」タブに移動します。
- ⚙️アイコンをタップして拡張機能の設定を開きます。
- **向きオフセットを設定**の値を`1`に増やします。

---

✅ 完了！ GNOME は BredOS 上で適切に設定されました。 🚀
