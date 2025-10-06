---
title: Android アプリを実行（ウェイドロイド）
description:
published: true
date: 2025-09-26T10:03:46.309Z
tags:
editor: markdown
dateCreated: 2025-09-21T08:40:19.752Z
---

# 1. はじめに

Waydroidは、Linux/GNU 上で Wayland を使って Android を実行するためのコンテナベースのソリューションです。 このガイドでは、インストールに必要な手順を説明します。 このガイドでは、インストールに必要な手順を説明します。 このガイドでは、インストールに必要な手順を説明します。 このガイドでは、インストールに必要な手順を説明します。

# 2. インストール

- Install Waydroid:

```
sudo pacman -S waydroid
```

## 2.1 RK3588

You need panthor enabled and setup follow [this guide](/how-to/how-to-setup-panthor). パンターを有効にしてセットアップする必要があります。 To do this follow [this guide](/how-to/how-to-setup-panthor).

- Install panthor image:

```
sudo pacman -S waydroid-panthor-image
```

- Initialize waydroid:

```
sudo waydroid init -f -i /usr/share/waydroid-extra/images
```

## 2.2 Generic ARM64/X86_64

- これにより、GAPPSバージョンのアンドロイドがダウンロードおよびインストールされます。

```
sudo waydroid init -s GAPPS
```

# 3. ウェイドロイドを有効にして開始

- ウェイドロイドの有効化と開始:

```
sudo systemctl enable --now waydroid-container
```

- 次にウェイドロイドコンテナを起動します。

```
ウェイドロイドセッション開始
```

# 4. アプリのインストール

- apk をダウンロードして実行:

```
waydroid app install <apk>.apk
```

# 4. アプリのインストール

ウェイドロイドはデフォルトで常にフルスクリーンで動作します。

- waydroidがデスクトップ環境ウィンドウマネージャと統合したい場合は、以下を実行してください。

```
waydroid props set persist.waydroid.multi_windows true
```

次にウェイドロイドセッションを再起動します。