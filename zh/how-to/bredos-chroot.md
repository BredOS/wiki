---
title: BredOS-Chroot utility
description: 一个从二级系统挂载到 BredOS 安装的简单工具
published: true
date: 2025-05-07T17:48:24.068Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

可用于“bredos-tools”软件包的一部分。

## 用法

```
用法：/usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

示例：
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

挂载给定的 Btrfs 分区与子卷和引导分区，
然后在系统中查找根。 退出chroot后净化。
```

假定你有一个系统失败的 SDCard, 在 /dev/sdb上可在 `lsblk` 中看见, 你可以运行:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

你会把根外壳进入破损的系统，方便维修。

一旦修理完成，您只需输入 `exit` 或 Ctrl + D 就可以关闭外壳，附加卡将被卸载。