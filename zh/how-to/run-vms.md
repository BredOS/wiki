---
title: 如何在 BredOS 上运行虚拟机
description:
published: true
date: 2025-09-13T09:21:19.167Z
tags: vm, ho-to
editor: markdown
dateCreated: 2024-10-05T22:12:39.679Z
---

# :ro火箭: 使用 Virt-Manager 在 BredOS 上运行虚拟机

本指南将帮助您在 BredOS 上使用 "virt-manager" 设置和管理虚拟机器。

## 📋 预设

在您开始之前，请确保您有以下内容：

- 网络连接 :glube_with_meridians：
- Sudo 权限 🔑

## 第 1 步：安装必需的软件包 📦

您需要安装 KVM 和 `virt-manager` 所需的软件包。

```bash
sudo pacman -Syu
sudo pacman -S virt-manager virt-viewer qemu-Base qemu-system-aarch64 edk2-aarch64 dnsmasq 
```

## 第 2 步：启用并启动 Libvirt 服务

一旦安装了软件包，启用并启动 `libvirtd` 服务：

```bash
sudo systemctl 启用 --now libvirtd
```

要验证服务正在运行：

```bash
sudo systemctl status libvirtd
```

## 第 3 步：将您的用户添加到"libvirt" 组 👥

为了避免需要 root 权限来管理 VM ，请将您的用户添加到 libvirt' 组：

```bash
sudo usermod -aG libvirt $(whoami)
```

将您自己添加到群组后，注销并重新登录以使更改生效。

## 第 4 步： 配置网络 :globe_with_meridians：

`virt-manager` 使用 `dnsmasq` 进行网络管理。 `virt-manager` 使用 `dnsmasq` 进行网络管理。 您可能想要确保使用 "libvirt" 的默认网络设置： `virt-manager` 使用 `dnsmasq` 进行网络管理。 您可能想要确保使用 "libvirt" 的默认网络设置：

```bash
sudo virsh net-start 默认
sudo virsh net-autostart
```

## 步骤 5：启动 Virt-Manager :desktop_compute：

现在已经设置了一切，你可以启动"病毒管理器"：

```bash
病毒管理器
```

这将打开`virt-manager`GUI，您可以在那里创建和管理虚拟机器。
![virt.jpg](/vms/virt.jpg)

## 步骤6：启用 XML 编辑

要启用 XML 编辑 (需要稍后) ，您需要打开 `virt-manager` 到编辑然后首选项并启用 XML 编辑
![xmlediting.jpg](/vms/xmlediting.jpg)

## 步骤7：创建虚拟机 :hammer_and_wrench：

1. 打开`virt-manager'。
   打开\`virt-manager'。
   ![virt.jpg](/vms/virt.jpg)
2. 点击**创建一个新的虚拟机器** ➕。
   ![virtnewvm.jpg](/vms/virtnewvm.jpg)
3. 选择安装源 (ISO 镜像或网络安装)。
   ![newvm.jpg](/vms/newvm.jpg)
4. 按照向导分配CPU、RAM和您的虚拟机存储。 ⚙️ ⚙️

> On the RK3588 you can allocate max 4 cores per vm due to the little big architecture
> {.is-warning}

![cpuram.jpg](/vms/cpuram.jpg)
![disk.jpg](/vms/disk.jpg)
5. On CPUs with the little.big architecture like the RK3588 you need to check "Customize configuration before install" and edit the xml responsible for allocating cpu cores
![finalstep.jpg](/vms/finalstep.jpg)
Click **Finish**
![vcpuxml0.jpg](/vms/vcpuxml0.jpg)
Open the **CPUs** configuration and then the **XML** tab
![vcpuxml1.jpg](/vms/vcpuxml1.jpg)
Locate `<vcpu>XYZ</vcpu>` and replace it with

```xml
<vcpu placement='static' cpuset='0-1'>2</vcpu>
```

如果cpu 设置是你想要使用的核心，则0-3是rk3588上的E核心，4-7是性能核心和核心数量。 在上面的例子中，vm将有两个核心，它们是死亡本身的高效核核心1和2。
![vcpuxml2.jpg](/vms/vcpuxml2.jpg) 在上面的例子中，vm将有两个核心，它们是死亡本身的高效核核心1和2。
![vcpuxml2.jpg](/vms/vcpuxml2.jpg)

6. 添加附带硬件和图形支持。 🖥️ 🖥️

返回虚拟机页面，按“添加硬件”。

![addhw.png](/vms/addhw.png)

然后从将显示的窗口中选择"视频"和模型选择, 选择"ramfb", 然后单击"完成"。

![gpu.png](/vms/gpu.png)

现在添加图形服务器，再次选择"添加硬件"，"图形"，然后单击"完成"。

![graphics.png](/vms/graphics.png)

Now for keyboard and mouse, repeat the same procedure by selecting:
"Input" -> "USB Keyboard"
and
"Input" -> "EvTouch USB Graphics Tablet"

![tab.png](/vms/kb.png)
![tab.png](/vms/tab.png)

7. 一旦配置完毕，启动虚拟机。 🟢 🟢

![startvm.jpg](/vms/startvm.jpg)

## 附加配置 :gear：

- 要通过命令行管理虚拟机，您可以使用 `virsh`：

```bash
病毒列表 --all
病毒start <vm-name>
病毒性关闭 <vm-name>
```

## 故障排除:hammer_and_wrench：

- **权限问题**：确保您的用户在 `libvirt` 组，并且`libvirtd` 服务正在运行。
- **Networking Issues**：如果VMs没有互联网接入，请确保默认的`virsh`网络正在运行。

## 🎉 结论

您在 BredOS 上成功地设置 `virt-manager` 并准备创建和管理虚拟机！
