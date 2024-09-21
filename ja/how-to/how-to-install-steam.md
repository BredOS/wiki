---
title: 🎮 ブレッドOSにSTEAMをインストールする方法
description: BredOS にSteamをインストールする簡単なガイドで、Panthor-enabled と、Panthor以外の両方の設定をステップバイステップで説明します。
published: true
date: 2024-09-08T10:37:48.498Z
tags: null
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 🎮 SteamをBredOSにインストールする方法

**Steam** のインストール方法に関するガイドへようこそ！ 以下の簡単な手順に従って、システムでSteamを起動して実行してください。

## 🛠️ 前提条件

> 注意: SteamはX11デスクトップでのみ動作するようです。 また、すべてのデバイス(主に非RK3588デバイス)で動作するわけではありません。
> {.is-info}

- **BredOS** をインストールして実行している必要があります。
- 必要に応じて、[**パンサー** ](/ja/how-to/how-to-setup-panthor) を有効にできますが、必須ではありません。

## 📥 インストール手順

### 🔄 BredOS の古い画像を使用する場合:

Steamと必要な翻訳レイヤーをインストールするには、**BredOS Multilib** リポジトリを追加する必要があります。 これを行うには、以下の手順に従ってください:

1. `bredos-multilib`パッケージをインストール

```
   sudo pacman -S bredos-multilib
```

2. 次を実行してパッケージデータベースを更新します。

```
   sudo pacman -Sy
```

---

### 🖥️ Steam インストール:

1. 端末🖥️を開きます。
2. Steamをインストールするには、次のコマンドを実行します。

```
   sudo pacman -S steam
```

3. コマンドを実行すると、オプションを選択するメッセージが表示されます。 設定に基づいて適切なオプションを選択してください:

   - まず、`lib32-vulkan-swrast`を選択します。

![steam\_libs\_selection.png](/steam_libs_selection.png)

- **Panthor**を有効にしている場合は、`steam-libs-any`を選択してください。
- **Panthor** が有効になっていない場合 (代わりに Panfork を使用)、`steam-libs-rk3588` を選択します。

4. インストールが完了するまでお待ちください。 🎉

## 🔄 Steam をアンインストールする

Steamをアンインストールし、設定をリセットして別のオプションを選択する必要がある場合:

```
sudo pacman -Rnscu steam-libs-any #or steam-libs-rk3588
```

## 🚀 Steamを起動する

インストールが完了したら、以下の手順でSteamを起動できます。

```
スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|
```

**ゲームを楽しもう！ 🎮✨**
