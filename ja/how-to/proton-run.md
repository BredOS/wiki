---
title: Proton-run
description: BredOS `proton-run` スクリプトの使用方法を簡単に説明します。
published: true
date: 2025-05-07T14:44:47.710Z
tags:
editor: markdown
dateCreated: 2025-05-07T14:44:47.710Z
---

# `proton-run`を使う

`proton-run`は最近リリースされたパッケージで、SteamのProton Experimentalを使ってBredOS ARM64の下でx86_64のWindowsアプリケーションを実行することができます。

## 要件

- An RK3588 system running BredOS.
- スチーム。 ([Guide here](en/how-to/how-to-install-steam))
- Steamを通じてProton Experimentalをインストールしました。
- パッケージ `proton-run` (`yay -S proton-run`) をインストールしました。

## 使用法

端末を開いて実行するだけです:

```
proton-run /path/to/your/windows/program.exe
```

多くのアプリが動作しません。 これを可能にするために3つのエミュレータがチェーンロードされています。
x86エミュレーションの状態です