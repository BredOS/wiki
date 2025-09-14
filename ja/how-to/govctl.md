---
title: ガバナンスの設定
description: govctl を使用してシステムガバナーを管理する
published: true
date: 2025-05-07T12:47:49.033Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.033Z
---

# GovCtl の使用

BredOS はデフォルトでパッケージ `bredos-govctl` にツール `govctl` を出荷します。
デフォルトで有効になっており、使用可能なバッテリー電力に応じてパフォーマンスを設定します。

ツールは継続的に指定された設定にガバナを設定し、オーバーライドや他のツールは機能しません。
これがワークフローの問題である場合は、パッケージをアンインストールしてください。

## デフォルトの動作

GovCtlはデフォルトで、オンボードバッテリがない場合、またはシステムが接続されている場合、接続されたすべてのデバイスで最大のパフォーマンスを確保します。

システムが十分な充電を保持しているが、プラグが差し込まれていない場合は、GPU速度とCPUブーストを制限し、パフォーマンスの大部分を維持します。

システムが十分な料金を持っていない場合(これが決定される20%がデフォルトポイントです)
システムは、性能と応答時間を損なうことで、電力引き込みを最小限に抑えます。
例えば、RK3588ボードは300mHzでのみ動作するようにします。

デフォルトを気に入らない場合は、すべて変更できます。

# 州知事の表示

現在適用されているガバナーを表示するには、 `govctl` を実行してください。root アクセスは必要ありません。

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

# 別のパワーセーブポイントの設定

ヘルプメニューが示すように、オプション`-p`を使用すると、`powersave`が適用されるポイントを再設定することができます。 これはデフォルトで20%であり、1named@@0に設定できます。 これはデフォルトで20%であり、1named@@0に設定できます。

以下のように再構成します。

```
sudo govctl -p 30
```

これにより、トリガーが30%に設定されます。

# 適用されるガバナーの変更

デフォルトでは、バッテリが接続されていない場合、またはバッテリが存在しない場合、システムは最大のパフォーマンスを維持します。
代わりに、より保守的な電源プロファイルを適用したい場合は、以下を実行してください。

```
sudo govctl -g conservant
```

プラグインされていなくても最大限のパフォーマンスを維持したい場合は、代わりに以下を実行してください:

```
sudo govctl -b performance
```

フラグ`-g`は、接続時に使用されるガバナを設定します。
Glag `-b` は、**プラグインされていない** 時に使われるガバナを設定します。

# バッテリー検出を無効にしています

バッテリー検出の無効化:

```
sudo govctl -d
```

常に「プラグイン」ガバナが常に適用されることを確認します。

これを元に戻すには、次を実行します。

```
sudo govctl -e
```