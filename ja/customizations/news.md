---
title: BredOS ニュース
description: この驚くほど複雑なソフトウェアをカスタマイズします
published: true
date: 2025-10-04T21:14:51.210Z
tags:
editor: markdown
dateCreated: 2025-10-04T21:13:09.732Z
---

# はじめに

BledOS ニュースは、シェルを開くたびに起動します。

BredOS はデフォルトで `~/.bashrc` と `/etc/profile.d/99-bredos-news.sh` を設定します。

ニュースのすべてのコピーがパーソナライズされます。

あなたは完全にそれのどの機能を望むだけでなく、それを完全にテーマに設定することができます。

## 設定と上書き

BredOS Newsはそれをカスタマイズするかなりの方法を提供しています。
Permenant (per-user) の設定は `~/.newsrc` で行うことができます。

デフォルトの空白設定は、アプリの最初の実行後に自動的に(再)生成されます。
書き込み時にデフォルトのファイルは次のようになります。

```
# BredOS-News Configuration

# Accent = "\033[38;5;129m"
# Accent_Secondary = "\033[38;5;104m"

# Hush_Updates = False
# Hush_Disks = False
# Hush_Smart = False
# Time_Tick = 0.1
# Time_Refresh = 0.25
# Onetime = False

# Shortcuts configuration

# shortcuts = {
#     "1": "bredos-config",
# }
```

`Accent` は基本的な色を設定します。`Accent_Secondary` はすべての詳細の色を設定します。
任意の ANSI エスケープシーケンスを適用することができます。
ANSI エスケープシーケンスと例の詳細については、[this link](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797) に従ってください。

### 機能を無効にしています

`Hush_Updates` はパッケージの更新セクションを完全に削除します。
`Hush_Disks` は添付されたメディアストレージの使用状況メモを削除します。
`Hush_Smart` はディスク障害の警告をミュートします。 これは使用しないでください。

### アニメーション時間の設定

`Time_Tick` はアニメーションのフレーム間の時間を設定します。
`Time_Refresh` はシステムの詳細が更新される頻度を設定します。
これらの値はすでに最高です。 これ以上もしくはcpuの使用を減らさないでください **スパイク** 。

`Onetime` はアニメーションループ、ショートカットシステム、端末のリサイズ機能を無効にします。

## ショートカット

`shortcuts` は設定可能なキー割り当ての辞書です。 あなたの端末のためのクイックダイヤル。

News はアニメーションをループさせていますが、設定されたキーのいずれかを押すと、シェルにキーを渡すのではなく、事前設定されたショートカットを起動します。

例のようにキーを設定すると、コマンドやPython関数を実行することができます。
ディレクトリや配管の変更などのシェル操作が完全にサポートされています。
特殊キーと組み合わせは現在サポートされていません。
記号がサポートされています。

## 環境の上書き

`HUSH_NEWS=1` を設定すると、BredOS ニュースが実行されなくなります。

`~/.hush_login` も同じ効果を持っています。