---
title: 在 BredOS 上运行虚拟机
description:
published: true
date: 2025-09-18T07:58:22.536Z
tags: vm, ho-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# 1. 简介

本指南将帮助您在 BredOS 上使用 "virt-manager" 设置和管理虚拟机器。

# 2. 必备条件

在您开始之前，请确保您有以下内容：

- 一个工作网络连接
- `sudo`权限

# 3. 安装

## 3.1 安装所需的软件包

- 要启动，您需要安装 `qemu` 和 `virt-manager` 所需的软件包。

```
sudo pacman -Syu virt-Manager virt-viewer qemu-base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

> 虽然`qemu`是你的超级用户，但`virt-manager`是一个基于GUI的工具来管理它。
> {.is-info}

## 3.2 启用并启动Libvirt服务

- 一旦安装了软件包，启用并启动 `libvirtd` 服务：

```bash
sudo systemctl 启用 --now libvirtd
```

- 要验证服务正在运行：

```bash
sudo systemctl status libvirtd
```

## 3.3 将您的用户添加到 `libvirt` 组

- 为了避免需要 root 权限来管理 VM ，请将您的用户添加到 libvirt' 组：

```bash
sudo usermod -aG libvirt $(whoami)
```

> 这将允许从用户层级管理虚拟机。 这可能是危险的！
> {.is-warning}

- 将您自己添加到群组后，注销并重新登录以使更改生效。

## 3.4 配置网络

- `virt-manager` 使用 `dnsmasq` 进行网络管理。 `virt-manager` 使用 `dnsmasq` 进行网络管理。 您可能想要确保使用 "libvirt" 的默认网络设置： `virt-manager` 使用 `dnsmasq` 进行网络管理。 您可能想要确保使用 "libvirt" 的默认网络设置： `virt-manager` 使用 `dnsmasq` 进行网络管理。 您可能想要确保使用 "libvirt" 的默认网络设置：

```bash
sudo virsh net-start 默认
sudo virsh net-autostart
```

## 3.5 启动虚拟管理器

- 现在已经设置了一切，你可以启动"病毒管理器"：

```bash
病毒管理器
```

- 这将打开`virt-manager`GUI，您可以在那里创建和管理虚拟机器。
  ![virt.jpg](/vms/virt.jpg)

![virt.jpg](/vms/virt.jpg)

> 如果你还没有将你的用户添加到组 `libvirt` 中，你现在需要输入你的密码。
> {.is-info}

## 3.6 启用 XML 编辑

- 要启用 XML 编辑 (需要稍后) ，您需要打开 `virt-manager` ，然后导航到 `Edit` 然后导航到 `Preferences` 和 \`启用 XML 编辑'。

# 4. 创建虚拟机

- 在 `virt-manager` 中，点击显示图标或导航到 `File` -> `Create 虚拟机器` 以创建一个新的虚拟机器。

- 选择安装源 (本地安装介质或网络安装)。

- 如果您选择本地安装介质，请使用向导来选择您的.iso文件。

- 按照向导分配CPU、RAM和您的虚拟机存储。 ⚙️

> 在 RK3588 上，由于小的大架构，您可以分配每vm 最多4个核。
> {.is-warning}

- 在点击“完成”之前，您需要检查“**在安装前自定义配置**”并编辑负责分配cpu核心的xml。

- 点击 `Finish`

一个新窗口打开，允许您在创建之前编辑虚拟机器的设置。 打开 CPU 配置，然后打开 XML 标签。

- Locate `<vcpu>XYZ</vcpu>` and replace it with:

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

> 如果`cpu set`，你可能想要使用的核心是RK3588上的 0-3 (E核心)，或用于性能核心的4-7。
> 在上面的例子中，虚拟机将有两个核，它们是效率核（死亡本身的核1和2）。
> {.is-info}

- 一旦配置完毕，启动虚拟机。 🟢

> 在那里，我们已经有了它。 现在你可以在 Bred 内部运行蓝色！
> {.is-success}

# 5. 附加配置

- 要通过命令行管理虚拟机，您可以使用 `virsh`：

```bash
病毒列表 --all
病毒start <vm-name>
病毒性关闭 <vm-name>
```


