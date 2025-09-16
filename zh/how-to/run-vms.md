---
title: 在 BredOS 上运行虚拟机
description:
published: true
date: 2025-09-16T10:47:11.442Z
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

![xmlediting.jpg](/vms/xmlediting.jpg)

## 3.7 创建虚拟机

- 打开\`virt-manager'。

打开\\`virt-manager'。
![virt.jpg](/vms/virt.jpg)

- 点击图标在新虚拟机下方屏幕截图上显示。

![virtnewvm.jpg](/vms/virtnewvm.jpg)

- 选择安装源 (ISO 镜像或网络安装)。
  ![newvm.jpg](/vms/newvm.jpg)

![newvm.jpg](/vms/newvm.jpg)

- 按照向导分配CPU、RAM和您的虚拟机存储。 ⚙️

![cpuram.jpg](/vms/cpuram.jpg)

> 在 RK3588 上，由于小的大架构，您可以分配每vm 最多4个核。
> {.is-warning}

- 创建您预置大小的虚拟磁盘。

![disk.jpg](/vms/disk.jpg)

- 在 CPU 上少量的。 ig 架构类似于RK3588，您需要检查“安装前自定义配置”并编辑负责分配cpu核心的xml。

![finalstep.jpg](/vms/finalstep.jpg)

- 点击 `Finish`

![vcpuxml0.jpg](/vms/vcpuxml0.jpg)

- 打开 CPU 配置，然后打开 XML 标签

![vcpuxml1.jpg](/vms/vcpuxml1.jpg)

- Locate `<vcpu>XYZ</vcpu>` and replace it with

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

- 如果cpu 设置是你想要使用的核心，则0-3是rk3588上的E核心，4-7是性能核心和核心数量。 在上面的例子中，vm将有两个核心，它们是死亡本身的高效核核心1和2。
  ![vcpuxml2.jpg](/vms/vcpuxml2.jpg) 在上面的例子中，vm将有两个核心，它们是死亡本身的高效核核心1和2。

![vcpuxml2.jpg](/vms/vcpuxml2.jpg)

- 添加附带硬件和图形支持。 🖥️

- 返回虚拟机页面，按“添加硬件”。

![addhw.png](/vms/addhw.png)

- 然后从将显示的窗口中选择"视频"和模型选择, 选择"ramfb", 然后单击"完成"。

![gpu.png](/vms/gpu.png)

- 现在添加图形服务器，再次选择"添加硬件"，"图形"，然后单击"完成"。

![graphics.png](/vms/graphics.png)

- 现在对于键盘和鼠标，通过选择以下方法重复相同的程序：
  `Input` -> `USB 键盘` 和 `Input` -> `EvTouch USB 图形平板`

![tab.png](/vms/kb.png)
![tab.png](/vms/tab.png)

- 一旦配置完毕，启动虚拟机。 🟢

![startvm.jpg](/vms/startvm.jpg)

> 在那里，我们已经有了它。 现在你可以在 Bred 内部运行蓝色！
> {.is-success}

## 3.8 额外配置

- 要通过命令行管理虚拟机，您可以使用 `virsh`：

```bash
病毒列表 --all
病毒start <vm-name>
病毒性关闭 <vm-name>
```

## 3.9 故障处理

- **权限问题**：确保您的用户在 `libvirt` 组，并且`libvirtd` 服务正在运行。
- **Networking Issues**：如果VMs没有互联网接入，请确保默认的`virsh`网络正在运行。

