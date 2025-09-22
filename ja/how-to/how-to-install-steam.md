---
title: BredOS にSTEAMをインストール
description: BredOS にSteamをインストールする簡単なガイドで、Panthor-enabled と、Panthor以外の両方の設定をステップバイステップで説明します。
published: true
date: 2025-09-18T07:12:38.577Z
tags:
editor: markdown
dateCreated: 2024-09-08T09:55:58.661Z
---

# 1. はじめに

**Steam** のインストール方法に関するガイドへようこそ！ 以下の簡単な手順に従って、システムでSteamを起動して実行してください。 以下の簡単な手順に従って、システムでSteamを起動して実行してください。

# 2. 前提条件

> この方法は、Rockchip RK35xx デバイスのためのものです!
> {.is-info}

- **BredOS** をインストールして実行している必要があります。
- 必要に応じて、[Panthor enabled](/how-to/how-to-setup-panthor) を使用できますが、必須ではありません。

# 3. インストール手順

## 3.1 自動

- 「bredos-config」ツールは、steamと適切なsteam-libをインストールする簡単な方法を提供します。 ツールを起動する ツールを起動する

```
sudo bredos-config
```

- 次に、`Packages` -> `Install Steam`に移動します。 するとスチームがインストールされます。 簡単ですよね？

## 3.2 手動で

### 3.2.1 古い BredOS イメージを使用する場合:

Steamと必要な翻訳レイヤーをインストールするには、**BredOS Multilib** リポジトリを追加する必要があります。 これを行うには、以下の手順に従ってください: これを行うには、以下の手順に従ってください:

- `bredos-multilib`パッケージをインストール

```
   sudo pacman -S bredos-multilib
```

- 次を実行してパッケージデータベースを更新します。

```
   sudo pacman -Sy
```

### 3.2.2 Steam インストール：

- Steamをインストールするには、次のコマンドを実行します。

```
   sudo pacman -S steam
```

- コマンドを実行すると、オプションを選択するメッセージが表示されます。 設定に基づいて適切なオプションを選択してください: 設定に基づいて適切なオプションを選択してください:

- まず、`lib32-vulkan-swrast`を選択します。

![steam_libs_selection.png](/steam_libs_selection.png)

- **Panthor**を有効にしている場合は、`steam-libs-any`を選択してください。

- **Panthor** が有効になっていない場合 (代わりに Panfork を使用)、`steam-libs-rk3588` を選択します。

- インストールが完了するまで待ち、すべてが設定されています。

# 4. Steamをアンインストール中

- Steamをアンインストールし、設定をリセットして別のオプションを選択する必要がある場合:

```
sudo pacman -Rnscu steam-libs-any #or steam-libs-rk3588
```

# 5. Steamを起動

- インストールが完了したら、以下の手順でSteamを起動できます。

```
スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|スチーム|
```

> ハッピーゲーム！
> {.is-success}

