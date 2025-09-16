---
title: 使用您的设备作为无线热点
description:
published: true
date: 2025-09-16T10:50:45.422Z
tags:
editor: markdown
dateCreated: 2024-09-08T10：33：46.772Z
---

# 1. 简介

本指南将向您展示如何使用 NetworkManager 设置 Wi-Fi 热点。

# 2. 必备条件

在您开始之前，请确保您：

- 支持 AP (访问点) 模式的 Wi-Fi 适配器

> 支持 AP (Access Point) 模式的适当设备包括Rock 5C，Rock 5B+， Khadas Edge 2, Khadas Vim 4, all Mekotronics R58 设备，以及Orange Pi 5B。
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

# 3. 安装

## 3.1 创建热点

您可以轻松使用 NetworkManager 命令行工具`nmcli` 创建热点。

- 列出您的网络设备以识别您将使用的 Wi-Fi 接口：

```bash
   nmcli 设备状态
```

- 示例输出

```
	DEVICE           TYPE      STATE                   CONNECTION      
	bridge0          bridge    connected               bridge0         
	tailscale0       tun       connected (externally)  tailscale0      
	lo               loopback  connected (externally)  lo              
	br-8a9f1336b961  bridge    connected (externally)  br-8a9f1336b961 
	br-aeeaf62e2336  bridge    connected (externally)  br-aeeaf62e2336 
	docker0          bridge    connected (externally)  docker0         
	virbr0           bridge    connected (externally)  virbr0          
	enp8s0           ethernet  connected (externally)  enp8s0          
	wlan0            wifi      disconnected            --   
```

- 使用以下命令创建热点：

```bash
   nmcli 设备 Wifi 热点ifname <wifi_interface> ssid <MyHotspot> 密码 <mypassword>
```

- 示例输出：

```
  Device 'wlan0' successfully activated with '4d090d70-fd85-45bc-bf36-a63846f3f805'. 
  Hint: "nmcli dev wifi show-password" shows the Wi-Fi name and password.
```

```
用您的实际接口名称替换<wifi_interface>`，比如`wlp2s0`或`wlan0`， 使用您想要的 SSID 的<MyHotspot>和 `<mypassword>的密码选择一个安全的密码。
```

> 如果出现以下错误，请使用 sudo 再次运行该命令
> “错误：无法设置 Wi-Fi 热点：无权控制网络。”
> {.is-info}

## 3.2 查看热点状态

- 一旦创建热点后，您可以通过运行来验证其状态：

```bash
nmcli 连接显示
```

- 示例输出

```
NAME                            UUID                                  TYPE       DEVICE          
Hotspot                         4d090d70-fd85-45bc-bf36-a63846f3f805  wifi       wlan0           
bridge0                         210b2bd8-1a6b-43e6-9ed1-4abc50324505  bridge     bridge0         
tailscale0                      27e86e0c-a8c7-4374-9083-51454c4b8b3e  tun        tailscale0      
lo                              f6ba586b-a4c4-49c1-a0f3-3154f8eae92b  loopback   lo              
br-8a9f1336b961                 9a3d08b3-6516-4071-9369-30311a48b55a  bridge     br-8a9f1336b961 
br-aeeaf62e2336                 ee78e282-1516-45df-a6ec-cdcb9d989030  bridge     br-aeeaf62e2336 
docker0                         c5f70ee8-5407-4510-8b61-6fc0f15c2e81  bridge     docker0         
virbr0                          12d1109a-64a4-4d07-b0a2-887f10145109  bridge     virbr0          
enp8s0                          184c8145-ca17-4258-b7db-7e32c298f424  ethernet   enp8s0
```

您应该看到在活动连接下列出的热点(在上面的例子中第二行)。

## 3.3 配置 IP 转发中

要通过热点共享您的互联网连接，您需要启用 IP 转发：

- 启用 IP 转发：

```bash
   sudo sysctl net.ipv4.ip_forward=1
```

- 编辑 `/etc/sysctl.d/99-sysctl.conf` 使其永久性：

```bash
   sudo nano /etc/sysctl.d/99-sysctl.conf
```

- 增加以下行：

```
   net.ipv4.ip_forward=1
```

## 3.4 停止热点

- 要停止热点，只需运行：

```bash
热点下的 nmcli 连接
```
