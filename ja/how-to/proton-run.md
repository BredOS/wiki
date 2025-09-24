---
title: Proton-run
description: BredOS `proton-run` スクリプトの使用方法を簡単に説明します。
published: true
date: 2025-07-22T00:13:45.447Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# 1. 要件

`proton-run`は最近リリースされたパッケージで、SteamのProton Experimentalを使ってBredOS ARM64の下でx86_64のWindowsアプリケーションを実行することができます。

# 2. 要件

- An RK3588 system running BredOS.
- スチーム。 スチーム。 スチーム。 スチーム。 スチーム。 ([Guide here](/how-to/how-to-install-steam))

# 3. インストール

## 2.1 SteamのProton Experimentalのインストール

Steamを開き、`Library`に移動します。 検索バーをクリックし、`proton` と入力します。 「Proton Experimental」を選択してインストールします。

> 陽子の他のバージョンは働かない。
> {.is-info}

## 2.2 proton-runのインストール

- `proton-run`を使う

```
yay -S proton-run
```

# 4. 使用法

- 端末を開いて実行するだけです:

```
proton-run /path/to/your/windows/program.exe
```

> 多くのアプリが動作しません。 これを可能にするために3つのエミュレータがチェーンロードされています。
> x86エミュレーションの状態です
> {.is-warning}
