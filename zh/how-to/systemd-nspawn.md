---
title: 使用系统生成的容器管理
description:
published: false
date: 2025-09-25T07:02:39.910Z
tags:
editor: markdown
dateCreated: 2025-09-25T07:02:39.910Z
---

# 2. 介绍信息

`systemd-nspawn`是一种轻量容器工具，它与系统一起设计，用于在严格隔离的环境中运行一个命令或操作系统环境。 通常被描述为“在steroid上的chroot， 它为测试或运行整个Linux发行版或以安全和受控制的方式最小的环境提供了方便的方式。

不同于完全虚拟化解决方案，例如QEMU或Docker等容器平台，`systemd-nspawn` 使用 Linux 命名空间和组来创建几乎没有间接费用的容器。

# 3. 创建容器模板

使用 n出生的容器可以从您的文件系统上的任何位置运行，但推荐的文件夹是 `/var/lib/miles` 。 在这个文件夹中，我们创建一个子文件夹来保持我们的 Linux/GNU rootf。 为了简化过程，这篇文章通过创建一个容器模板向您提供指导。 该模板文件夹的内容可以复制到一个新的位置并用作一个新的容器环境。

- 切换到根目录：

```
sudo su
```

- 然后将目录更改为 `/var/lib/byes`：

```
cd /var/lib/mecherches
```

- 并创建模板文件夹：

```
mkdir 模板
```

由于容器可以持有任何发行版的rootf，您可以选择相对自由。 我们提供了一个最低发行量的油球清单，如Debian、Ubuntu和BredOS等； 不过，请注意，本条是专门针对BredOS容器的。

> 任何需要在容器内运行的命令，如果您不使用 BredOS，则必须根据您的发行版变量进行调整。
> {.is-info}

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) 查找您选择的版本，然后下载 .tar.gz 为您的 CPU 架构。
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) 向下滚动并点击您想要下载的版本，然后为您的 CPU 架构下载.tar.gz。
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) 向下滚动并在集装箱基地或集装箱最低基地之间选择。
- [Arch Linux](https://archlinux.org/download/) 选择您附近的镜像，然后下载 .tar.zst文件。
- [Arch Linux ARM](https://archlinuxarm.org/os/) 下载带有arch64 或 armv7 标签的 .tar.gz 文件。
  {.links-list}

当你下载了你的rootfs tarball后，我们需要提取它。 在这个示例中，我们下载了Arch Linux ARM tarball，并稍后将其转换为 BredOS 。

- 仍然作为根提取tarball到 `/var/lib/orges/template`：

```
sudo tar -xzf <your distro's tarball of choice> -C /var/lib/orges/template
```

- 文件夹`template`的内容看起来像这样：

```
ls template/
bin boot dev etc home lib mnt lease proc root runs sbin srv sys tmp usr var
```

