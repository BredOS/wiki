---
title: DRMで保護されたコンテンツを再生する方法(widevineをインストール)
description: Widevine プラグインをインストールすることで、DRMで保護されたコンテンツをブレッドOS上で再生できるようにする方法を学びます。
published: true
date: 2025-09-15T09:17:04.241Z
tags:
editor: markdown
dateCreated: 2024-08-28T05:58:27.563Z
---

# 1. はじめに

Widevineプラグインをインストールすることで、DRMで保護されたコンテンツをブレッドOS上で再生できるようにする方法を学びます。

# 2. Widevine

## 2.1 Widevine のインストール

- 端末を開き、次のコマンドを実行してWidevineをインストールします。

```
sudo pacman -S widevine-aarch64
```

## 2.2 システムを再起動

- インストール後、変更が反映されるようにシステムを再起動します。

## 2.3 Netflixの設定

- Netflixを視聴するには、ユーザーエージェントを騙す必要があります。 次のユーザーエージェント文字列を使用します。 次のユーザーエージェント文字列を使用します。

```
Mozilla/5.0 (X11; COS aarch64 15236.80.0) AppleWebKit/537.36 (KHTML, Geckoなど) Chrome/109.0.5414.125 Safari/537.36
```

> この Firefox 拡張機能をインストールすることで、ユーザーエージェントを簡単に偽装できます: [User-Agent String Switcher](https://addons.mozilla.org/en-GB/firefox/addon/user-agent-string-switcher/)
> {.is-info}


