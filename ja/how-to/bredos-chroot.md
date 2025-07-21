---
title: BredOS-Chroot utility
description: セカンダリシステムからBredOSインストールにマウントしてクロートする簡単なツール
published: true
date: 2025-05-07T17:48:24.068Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

`bredos-tools`パッケージの一部として利用できます。

## 使用法

```
Usage: /usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

Example:
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

Mounts the given Btrfs partition with subvolumes and the boot partition,
then chroots into the system. Cleans up after exiting chroot.
```

/dev/sdbで`lsblk`から表示される、失敗したシステムのSDカードがあるとすると、以下を実行できます。

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

壊れたシステムに根の殻が入り込み修理が容易になります

修復が完了したら、`exit` または Ctrl + D と入力するだけでシェルを閉じることができ、添付されたカードはアンマウントされます。