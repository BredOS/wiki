---
title: BredOS-Chroot utility
description: セカンダリシステムからBredOSインストールにマウントしてクロートする簡単なツール
published: true
date: 2025-09-15T06:05:42.545Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. インストール

`bredos-tools`パッケージの一部として利用できます。 デフォルトでは、これをインストールする必要があります。 インストールされていない場合

```
sudo pacman -S bredos-tools
```

## 2. 使用法

ヘルプメッセージを表示するには、パラメータなしで `bredos-chroot` を実行します。

```
Usage: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Example:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Mounts the given Btrfs partition with subvolumes and the boot partition,
then chroots into the system. Cleans up after exiting chroot.
```

## 3. 例

失敗したシステムのSDカードが **/dev/sdb** の `lsblk` から表示されていると仮定すると、以下を実行できます。

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

`/dev/sdb3`がブレッドOSのルートパーティションであり、`/dev/sdb2`がブレッドOSのブートパーティションです。

これは、壊れたシステムにルートシェルを取得し、修復を容易にします。

修復が完了したら、`exit` または Ctrl + D と入力するだけでシェルを閉じることができ、添付ファイルシステムがアンマウントされます。