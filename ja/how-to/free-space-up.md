---
title: 🧹💾 ディスク領域のクリーンアップガイド
description: 時間が経つにつれて、あなたのシステムは貴重なスペースを占める不要なファイルを蓄積するかもしれません。 このガイドでは、BredOS システムのディスク領域を取り戻す方法をいくつかご紹介します。 🖥️✨ 🖥️✨
published: true
date: 2024-09-21T09:03:53.416Z
tags:
editor: markdown
dateCreated: 2024-09-20T20:26:57.698Z
---

# BredOS ディスク領域クリーンアップガイド 🧹💾

時間が経つにつれて、あなたのシステムは貴重なスペースを占める不要なファイルを蓄積するかもしれません。 このガイドでは、BredOS システムのディスク領域を取り戻す方法をいくつかご紹介します。 🖥️✨ 🖥️✨

---

## 📚 目次

- クリーンパッケージキャッシュ📦
- 古いログファイルを消去する 📝
- BleachBit :spongeを使用
- ユーザーキャッシュをクリア 🏠
- 大きなファイルとディレクトリを検索 📂

---

## クリーンパッケージキャッシュ📦

パッケージをインストールまたは更新する際、**Pacman** は `/var/cache/pkg/` にキャッシュされたコピーを保持し、再インストールを高速化します。 ただし、これらのキャッシュされたパッケージは蓄積され、ディスク領域を使用する可能性があります。 ただし、これらのキャッシュされたパッケージは蓄積され、ディスク領域を使用する可能性があります。

### キャッシュサイズを確認する 📏

パッケージキャッシュの大きさを確認するには、以下を実行します。

```bash
du -sh /var/cache/pacman/pkg/
```

### 手動クリーンアップ :wasteバスケット:

インストールされていないキャッシュされたパッケージを手動で削除することができます:

```bash
sudo pacman -Sc
```

### Paccache で自動クリーンアップ 🔄

**paccache** を使用すると、各パッケージの最新の 3 つのバージョンのみを保持できます。

1. 必要なツールをインストールします:
   ```bash
   sudo pacman -S pacman-contrib
   ```
2. トランザクションごとに自動的にクリーンアップするには、Pacman フックを設定します。
   ```bash
   sudo nano /usr/share/libalpm/hooks/pacche.hook
   ```
   ファイルに次の内容を追加します:
   ```bash
   [Trigger]
   Operation = Upgrade
   Operation = Install
   Operation = Remove
   Type = Package
   Target = *

   [Action]
   Description = Cleaning pacman cache with paccache…
   When = PostTransaction
   Exec = /usr/bin/paccache -r
   ```
   **Ctrl + S**でファイルを保存し、**Ctrl + X**で終了します。

---

## 古いログファイルを消去する 📝

システムログは時間の経過とともにかなりのスペースを占める可能性があります。 ログのサイズは次のとおりです。 ログのサイズは次のとおりです。

```bash
journalctl --disk-usage
```

### 以前のログをクリーンアップ 🧼

3日前のログを削除するには:

```bash
sudo journalctl --vacuum-time=3d
```

---

## BleachBit :spongeを使用

**BleachBit** は強力なツールで、システムのジャンク、空きディスクスペースをクリーンアップし、プライバシーを保護します。 BleachBit [here](https://www.bleachbit.org/) の使用方法の詳細を学ぶことができます。 BleachBit [here](https://www.bleachbit.org/) の使用方法の詳細を学ぶことができます。

---

## ユーザーキャッシュをクリア 🏠

システムを使用すると、キャッシュはホームディレクトリに蓄積されます。 キャッシュフォルダのサイズは次のとおりです。 場合によっては、大きなファイルが不必要にスペースを占有することがあります。 それらを識別するために使用できるツールは次のとおりです。 それらを識別するために使用できるツールは次のとおりです。

```bash
sudo du -sh ~/.cache/
```

### キャッシュをクリア 🧹

すべてのキャッシュファイルを削除するには:

```bash
rm -rf ~/.cache/*
```

---

## 大きなファイルとディレクトリを検索 📂

場合によっては、大きなファイルが不必要にスペースを占有することがあります。 それらを識別するために使用できるツールは次のとおりです。 それらを識別するために使用できるツールは次のとおりです。

### コンソールツール ⌨️

- **du** — ディスク使用状況の検査官。\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- **gdu** — コンソールインターフェイスを備えたディスク使用量アナライザ。\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`

- **ncdu** — ncurses disk usage analyzer.\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`

### グラフィカルツール 🖼️

- **Filelight** — 同心円リングによるインタラクティブなディスク使用量マップ。\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`

- **GNOME Disk Usage Analyzer(baobab)** — GNOME用ディスク使用量アナライザ。\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer(baobab)** — GNOME用ディスク使用量アナライザ。\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`

- **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`

---

空き容量を増やし、BredOS システムをスムーズに稼働させてください。 💪✨ 📚 目次
