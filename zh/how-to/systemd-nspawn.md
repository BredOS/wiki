---
title: 使用系统生成的容器管理
description:
published: false
date: 2025-09-25T08:18:04.446Z
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

- [Ubuntu-base](https://cdimage.ubuntu.com/ubuntu-base/releases/) 查找您选择的版本，然后下载 `.tar.gz` 用于您的 CPU 架构。
- [Debian genericcloud](https://cloud.debian.org/images/cloud/) 向下滚动并点击您想要下载的版本，然后下载 `.tar.gz` 作为您的 CPU 架构。
- [Fedora Container Base](https://fedoraproject.org/misc#minimal) 向下滚动并在`Container Base`或`Container Minimal Base`之间选择。
- [Arch Linux](https://archlinux.org/download/) 选择你附近的镜像，然后下载 `.tar.zst` 文件。
- [Arch Linux ARM](https://archlinuxarm.org/os/) 用 `latest` 和 `arch64` 或 `armv7` 标签下载.tar.gz文件。
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

- 要进入容器，请运行：

```
systemd-nspawn --machine="Template" --directory=/var/lib/organes/template
```

参数`--machine`定义容器的名称，而`--directory`指向容器的位置。 To exit the container either use <kbd>Ctrl</kbd> + <kbd>D</kbd> or click <kbd>Ctrl</kbd> + <kbd>]</kbd> three times within one second.

我们想要在容器内做的第一件事是初始化我们的包管理器并更新系统。

- 要做到这一点，请运行：

```
pacman-key --init
pacman-key --populate
pacman -Syu
```

> 如果您在解析主机名时遇到问题，请从主机系统中移除文件 `/var/lib/orges/template/etc/resolv.conf` 。
> {.is-danger}

- 然后，我们需要移除像内核和固件这样的不间断的东西：

```
pacman -R linux-aarch64 linux-firmware
```

- 要将容器转换为 BredOS，请运行以下操作：

```
pacman-key --recv-keys 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
pacman-key --lsign-key 77193F152BDBE6A6 BF0740F967BA439D DAEAD1E6D799C638 1BEF1BCEBA58EA33
echo -e '# --> BredOS Mirrorlist <-- #\n\n# BredOS Main mirror\nServer = https://repo.bredos.org/repo/$repo/$arch\n' | tee /etc/pacman.d/bredos-mirrorlist
```

- 这里编辑镜像文件：

```
nano /etc/pacman.conf
```

- 并在结尾处添加以下内容：

```
[BredOS-any]
包含= /etc/pacman.d/bredos-mirrorlist

[BredOS]
包含= /etc/pacman.d/bredos-mirrorlist
```

- 最终开始转换：

```
pacman -Syu bred-os-release BredOS-any/lsb-release bredos-logo
```

- 可选，安装bredos-config 和/或bredos-news：

```
pacman -Sy bredos-config bredos-news
```

# 4. 使用虚拟网络创建容器

我们在第2节中创建的容器。 创建容器模板](#h-3-create-container-template) 使用了您的主机系统网络。 如果您喜欢在容器上安装虚拟网络设备，例如因为您想要使用 [Open vSwitch](/en/how-to/open-vswitch)，请做以下操作。

- 如果你想要在一个新容器上这样做，请克隆它：

```
mkdir /var/lib/miles/template-veth
rsync -avP /var/lib/miles/template/* /var/lib/meches/template-veth/
```

为了简化本指南，我们将继续使用在 [2] 创建的模板。 创建容器模板](#h-3-create-container-template)。

- 首先，像以前一样输入容器：

```
systemd-nspawn --machine="Template" --directory=/var/lib/organes/template
```

为了保持系统主题，我们使用 `systemd-network` 来配置我们的虚拟网络设备。

- 创建两个配置文件：

```
触摸/etc/systemd/network/80-container-host0.network
nano /etc/system/network/99-wolVeth.network
```

- 将以下内容粘贴到配置文件：

```
[Match]
name=host0

[Network]
Address=<containers ip address> example -> 192.168.100/24
Gateway=<gateway of that network> 示例 -> 192.168。
DNS=<DNS Servers address> 示例-> 9.9.9.9
#DHCP=yes -> 或评论地址，网关和DNS以及取消评论DHCP以自动分配地址。
```

- 最后，开启“system-network”：

```
systemctl 启用 system-networkd
```

要让容器启动该服务，它需要启动(之前的命令更像是根目录)。 我们通过使用 `--boot` 参数来缓解这个问题。

```
systemd-nspawn --machine="模板" --directory=/var/lib/organes/template --boot
```

这将引导容器并将您放入登录提示。 此处无法登录根目录，所以您要么先创建用户，然后才能进入容器，要么继续使用 [4。 将容器作为服务运行](#h-4-run-container-as-a-service)。

- 要创建用户，请在容器内运行以下内容：

```
useradd <your username here>
passwd <your username here>
```

# 🚀 4. 将容器作为服务运行
