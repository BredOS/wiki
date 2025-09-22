---
title: ガバナンスの設定
description: govctl を使用してシステムガバナーを管理する
published: true
date: 2025-09-15T09:02:10.135Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.033Z
---

# 1. はじめに

BredOS はデフォルトで、`govctl`ツールをパッケージ`bredos-govctl`で出荷します。
デフォルトで有効になっており、使用可能なバッテリー電力に応じてパフォーマンスを設定します。
デフォルトで有効になっており、使用可能なバッテリー電力に応じてパフォーマンスを設定します。

- インストールされていない場合は、次のコマンドでインストールします。

```
BredOS はデフォルトでパッケージ `bredos-govctl` にツール `govctl` を出荷します。
デフォルトで有効になっており、使用可能なバッテリー電力に応じてパフォーマンスを設定します。
デフォルトで有効になっており、使用可能なバッテリー電力に応じてパフォーマンスを設定します。
```

ツールは継続的に指定された設定にガバナを設定し、オーバーライドや他のツールは機能しません。

- これがワークフローの問題である場合は、パッケージをアンインストールしてください。

```
GovCtl の使用
```

## デフォルトの動作

GovCtlはデフォルトで、オンボードバッテリがない場合、またはシステムが接続されている場合、接続されたすべてのデバイスで最大のパフォーマンスを確保します。

システムが十分な充電を保持しているが、プラグが差し込まれていない場合は、GPU速度とCPUブーストを制限し、パフォーマンスの大部分を維持します。

システムが十分な料金を持っていない場合(20%がこの決定のデフォルトしきい値です)。 性能と応答時間を犠牲にして消費電力を最小限に抑えます

> 例えば、RK3588ボードは300mHzでのみ動作するようにします。
> {.is-info}
> {.is-info}

デフォルトを気に入らない場合は、すべて変更できます。

## 1.2 州知事の表示

- 現在適用されているガバナーを表示するには、 `govctl` を実行してください。root アクセスは必要ありません。

```
govctl
```

```
[bill88t@icu | ~]> govctl

---------------------------------------
Currently applied governor: performance
---------------------------------------

usage: govctl [-h] [-g {powersave,conservative,performance}]
              [-b {powersave,conservative,performance}] [-e] [-d]
              [-p POWERSAVE_PERCENT]

Governor configuration tool

options:
  -h, --help            show this help message and exit
  -g, --set-governor {powersave,conservative,performance}
                        Set desired governor
  -b, --set-battery-governor {powersave,conservative,performance}
                        Set desired governor while running on battery power
  -e, --enable-battery-detection
                        Enable battery state detection
  -d, --disable-battery-detection
                        Disable battery state detection
  -p, --powersave-percent POWERSAVE_PERCENT
                        Percentage at which powersave triggers
```

## 別のパワーセーブポイントの設定

ヘルプメニューが示すように、オプション`-p`を使用すると、ガバナー`powersave`が適用されるポイントを再設定できます。 デフォルトでは、これは20%であり、1named@@0に設定できます。 デフォルトでは、これは20%であり、1named@@0に設定できます。

- 以下のように再構成します。

```
sudo govctl -p 30
```

これにより、トリガーが30%に設定されます。

## 1.4 適用されたガバナの変更

デフォルトでは、バッテリが接続されていない場合、またはバッテリが存在しない場合、システムは最大のパフォーマンスを維持します。
代わりに、より保守的な電源プロファイルを適用したい場合は、以下を実行してください。

- フラグ`-g`は、接続時に使用されるガバナを設定します。 システムの電源オフ時に「保守的」にしたい場合: システムの電源オフ時に「保守的」にしたい場合:

```
sudo govctl -g conservant
```

- フラグ`b`は、**ない**ときに使われるガバナを設定します。 システムがバッテリー切れになっているときに「パフォーマンス」にしたい場合:

```
sudo govctl -b performance
```

## バッテリー検出を無効にしています

- バッテリー検出の無効化:

```
sudo govctl -d
```

これにより、「プラグイン」ガバナが常に適用されることが保証されます。

- これを元に戻すには、次を実行します。

```
sudo govctl -e
```