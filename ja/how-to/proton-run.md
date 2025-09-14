---
title: Proton-run
description: BredOS `proton-run` スクリプトの使用方法を簡単に説明します。
published: true
date: 2025-09-13T09:47:37.755Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# windows アプリの実行にproton-runを使用する

「proton-run」ツールは最近リリースされたパッケージで、SteamのProton Experimentalを使用して、BredOS ARM64の下でx86_64のWindowsアプリケーションを実行することができます。

## 1. 要件

- An RK3588 system running BredOS.
- スチーム。 スチーム。 ([Guide here](/how-to/how-to-install-steam))

## 2. インストール

### 2.1 SteamのProton Experimentalのインストール

Steamを開き、`Library`に移動します。 検索バーをクリックし、`proton` と入力します。 「Proton Experimental」を選択してインストールします。 陽子の他のバージョンは働かない。

### 2.2 proton-runのインストール

コマンドで `proton-run` をインストールする

```
yay -S proton-run
```

## 3. 使用法

端末を開いて実行するだけです:

```
proton-run /path/to/your/windows/program.exe
```

> 多くのアプリが動作しません。 これを可能にするために3つのエミュレータがチェーンロードされています。
> x86エミュレーションの状態です
> {.is-warning}
