---
title: BredOS-Chroot 实用程序
description: 一个从二级系统挂载到 BredOS 安装的简单工具
published: true
date: 2025-09-15T06:05:42.545Z
tags:
editor: markdown
dateCreated: 2025-05-07T17:48:24.068Z
---

# BredOS-Chroot

## 1. 安装

- `bredos-chroot` 可以作为`bredos-tools`软件包的一部分使用。 默认情况下应该安装。 如果不安装它

```
sudo pacman -S bredos-tools
```

## 2. 用法

- 运行"bredos-chroot" 时没有任何参数来显示帮助消息。

```
用法：/usr/bin/bredos-chroot <btrfs_partition> <boot_partition>

示例：
  /usr/bin/bredos-chroot /dev/sdb3 /dev/sdb2

挂载给定的 Btrfs 分区与子卷和引导分区，
然后在系统中 chroot。退出 chroot 后清理。
```

## 3. 示例

- 假定你有一个系统失败的SDCard, 在 **/dev/sdb**上可见, 你可以运行:

```
sudo bredos-chroot /dev/sdb3 /dev/sdb2
```

> `/dev/sdb3` 是你的 BredOS 根分区，而`/dev/sdb2` 是你的 BredOS 引导分区。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

- 这将获得一个根外壳进入破损的系统，便于维修。 这将获得一个根外壳进入破损的系统，便于维修。 一旦修理完成，您只需输入 `exit` 或 Ctrl + D 键就可以关闭外壳，附加的文件系统将被卸载。 这将获得一个根外壳进入破损的系统，便于维修。 一旦修理完成，您只需输入 `exit` 或 Ctrl + D 键就可以关闭外壳，附加的文件系统将被卸载。 这将获得一个根外壳进入破损的系统，便于维修。 一旦修理完成，您只需输入 `exit` 或 Ctrl + D 键就可以关闭外壳，附加的文件系统将被卸载。