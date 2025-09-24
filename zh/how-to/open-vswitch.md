---
title: 如何管理虚拟开关
description:
published: true
date: 2025-09-24T12:11:02.185Z
tags:
editor: markdown
dateCreated: 2025-09-24T11：30：44.331Z
---

# 2. 介绍信息

Open vSwitch (OVS) 是一个开源、多层虚拟开关，旨在启用高级网络自动化，同时支持标准管理接口和协议。 它主要用于虚拟环境，以便利虚拟机之间以及虚拟机与物理网络之间的通信。

# 1. 安装

- 可以通过运行此命令来安装OVS：

```
sudo pacman -S openvswitch
```

- 安装成功后，我们需要启用和启动OVS服务：

```
sudo systemctl 启用 --now ovs-vswitchd
```

# 4. 创建 vSwitch

OVS及其开关(es)可以使用工具`ovs-vscl`来管理。

- 要创建一个新的开关运行：

```
sudo ovs-vsctl add-br <your switch name here>
```

请用您选择的名称替换`<your switch name here>`。

# 🚀 4. 连接虚拟网络设备

## 4.1 手动的

虚拟网络设备可以通过您的超访问器或通过容器手动创建。 它们将出现并发挥物理网络设备的功能。

- 要列出所有网络设备运行：

```
ip 一个
```

- 下面的示例输出可以看到三个设备：

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp49s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master ovs-system state UP group default qlen 1000
    link/ether 00:48:54:20:41:e0 brd ff:ff:ff:ff:ff:ff
    altname enx0048542041e0
    inet6 fe80::248:54ff:fe20:41e0/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
3: ve-databaselCjq@if2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master ovs-system state UP group default qlen 1000
    link/ether 82:22:48:3a:2b:1a brd ff:ff:ff:ff:ff:ff link-netnsid 4
    altname ve-databaseserver.dmz
    inet 169.254.19.70/16 metric 2048 brd 169.254.255.255 scope link ve-databaselCjq
       valid_lft forever preferred_lft forever
    inet 192.168.244.177/28 brd 192.168.244.191 scope global ve-databaselCjq
       valid_lft forever preferred_lft forever
```

在此示例中，我们使用 `ve-databaselCjq`，它是一个虚拟网络设备，是从系统生成的容器中生成。

- 要将其连接到我们的v开关，请运行：

```
sudo ovs-vsctl 附加端口 <your switch name here> ve-databaselCjq
```

- 如果你想要将该适配器的数据包标记为特定的vlan，使用`tag`参数：

```
sudo ovs-vsctl 附加端口 <your switch name here> ve-databaselCjq 标签=<your vlan id tag here>
```

## 4.1 自动通过 libvirt

如果您跟随[本指南](/how-to/run-vms)创建带有qemu/libvirt的超高维度堆栈， 您可以将您新创建的开关添加到 libvirt 已知的网络。 这允许您在GUI中选择您的 vSwitch ，您的 VM 虚拟网络设备将自动添加到启动后的 vSwitch 中。

- 启动 `virt-manager` 并右键点击 `QEMU/KVM` ，该屏幕截图中标记为蓝色。 然后点击“详细信息”。

![main.png](/vswitch/main.png)

在新窗口中，切换到标签`虚拟网络`，然后点击左下角的 <kbd>+</kbd> 登录。

- 然后切换到 `XML` 选项卡，然后将内容替换为：

```
<network>
  <name><your switch name here></name>
  <forward mode='bridge'/>
  <bridge name='<your switch name here>'/>
  <virtualport type='openvswitch'/>
  <portgroup name='vlan-01' default='yes'>
  </portgroup>
  <portgroup name='vlan-02'>
    <vlan>
      <tag id='2'/>
    </vlan>
  </portgroup>
</network>
```

- Replace `<your switch name here>` twice in the given config. 使用 `portgroup`-tag，你可以定义你想要在开关上使用的vlan。

![network.png](/vswitch/network.png)

# 🔄 3. 将 vSwitch 连接到物理网络

如果您想要将您的 vSwitch 连接到物理网络，您必须使用物理网络设备。

> 请注意，使用过的网络设备必须**没有**指定IP地址！
> {.is-info}

- 若要从上面的示例输出添加 `enp49s0` ，请运行：

```
sudo ovs-vsctl 附加端口 <your switch name here> enp49s0
```

如果您只有一个物理网络设备和/或想要将它用于您的主机网络， 您必须将 IP 地址分配给vSwitch 而不是物理网络设备。 这可以使用任何工具，例如网络管理员的图形界面或通过系统进行。

# 5. 通过互联网连接两个vSwitch

如果您在互联网上有两个通过 VPN 连接的设备，可以连接他们的 vSwitch。 这使得这些vSwitch上的设备可以不再配置地相互通信。 如果您的 vSwitch 已连接到物理开关，甚至可以通过互联网连接到物理设备。 这对许多目的都是有用的。

- 在两个主机上运行以下内容：

```
sudo ovs-vsctl 附加端口 <your switch name here> vxlan0 - 设置接口 vxlan0 类型=vxlan 选项:remote_ip=<IP address of other host>
```

As always, replace `<your switch name here>` with the name of your switch, and `<IP address of other host>` with the IP address of the host with the other vSwitch. 净化它；您已连接的设备现在可以在互联网上安全通信。

> 如果您的客户端能够相互控制，但是进一步的通信不起作用，这可能是一个MTU问题。
> {.is-danger}

## 6.1 解决MTU问题

MTU 定义了每个传输数据包的最大尺寸。 虽然ping 数据包通常不会填充到这个最大值，“real”通信就是这样的。 默认的 MTU 是 1500 字节； 如果你通过隧道发送了一个这么大的数据包，隧道本身需要添加诸如源地址和目的地址等信息。 这可能超过 MTU，导致数据包被分割，这可能会导致您客户的通信出现问题。 为了解决这个问题，只需将您客户端的 MTU 降低到1 200字节。 此调整可以通过您的DHCP服务器或手动进行。
