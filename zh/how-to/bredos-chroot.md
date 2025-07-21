---
title: BredOS-Chroot 实用程序
description: 一个从二级系统挂载到 BredOS 安装的简单工具
published: true
date: 2025-05-07T17:48:24.068Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

可用作 `bredos-tools` 软件包的一部分。

## 用法

```
用法：/usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

示例：
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

挂载给定的 Btrfs 分区与子卷和引导分区，
然后在系统中 chroot。退出 chroot 后清理。
```

假定你有一个系统故障的 SD 卡，在 /dev/sdb 上可在 `lsblk` 中看见，你可以运行：

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

你会进入根 shell 进入损坏的系统，方便维修。

一旦修理完成，您只需输入 `exit` 或 Ctrl + D 就可以关闭 shell，挂载的设备将被卸载。