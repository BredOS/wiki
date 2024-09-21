---
title: 🎥 DRM保護されたコンテンツを再生する方法(widevineをインストール)
description: Widevine プラグインをインストールすることで、DRMで保護されたコンテンツをブレッドOS上で再生できるようにする方法を学びます。
published: true
date: 2024-09-20T14:44:32.766Z
tags: null
editor: markdown
dateCreated: 2024-08-28T05:58:27.563Z
---

# 🎥 DRM保護されたコンテンツを再生する方法(widevineをインストール)

Widevineプラグインをインストールすることで、DRMで保護されたコンテンツをブレッドOS上で再生できるようにする方法を学びます。

## 🛠️ Widevine をインストールする手順

1. **🔧 Install Widevine**\
   ターミナルを開き、次のコマンドを実行してWidevineをインストールします。

```
sudo pacman -S widevine-aarch64
```

2. **🔄 システムを再起動**\
   インストール後、システムを再起動して変更を有効にします。

3. **🍿 Netflix用のセットアップ**
   Netflixを視聴するには、ユーザーエージェントが必要です。 次のユーザーエージェント文字列を使用します。

```
Mozilla/5.0 (X11; COS aarch64 15236.80.0) AppleWebKit/537.36 (KHTML, Geckoなど) Chrome/109.0.5414.125 Safari/537.36
```

このFirefox拡張機能をインストールすることで簡単にユーザーエージェントを偽装できます: [User-Agent String Switcher](https://addons.mozilla.org/en-GB/fireox/addon/user-agent-string-switcher/)
