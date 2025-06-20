---
title: 如何使用您的设备作为无线热点
description:
published: true
date: 2024-09-08T10:55:29.082Z
tags:
editor: markdown
dateCreated: 2024-09-08T10：33：46.772Z
---

# :natirna_bars：如何使用 NetworkManager 设置热点

本指南将向您展示如何使用 NetworkManager 设置 Wi-Fi 热点。

## 🛠️ 前提条件

在您开始之前，请确保您：

- :satellite_atirna: 一个 Wi-Fi 适配器支持AP(接入点) 模式

> 支持 AP (Access Point) 模式的适当设备包括Rock 5C，Rock 5B+， Khadas Edge 2, Khadas Vim 4, all Mekotronics R58 设备，以及Orange Pi 5B。
> {.is-info}
> {.is-info}
> {.is-info}

## 创建热点

您可以轻松使用 NetworkManager 命令行工具`nmcli` 创建热点。

1. **列出您的网络设备** 以识别您将使用的 Wi-Fi 接口：

   ```bash
   nmcli 设备状态
   ```

2. **使用以下命令创建热点** (替换`wifi_interface` 用您的实际接口名称，例如`wlp2s0` 或 `wlan0`)：

   ```bash
   nmcli 设备 wifi 热点ifname wifi_interface ssid MyHotspot 密码"mypassword"
   ```

   此命令将：

   - 📝 使用 SSID `MyHotspot` 创建热点
   - 🔑 设置密码为`mypassword`

> 如果出现以下错误，请使用 sudo 再次运行该命令
> “错误：无法设置 Wi-Fi 热点：无权控制网络。”
> {.is-info}

## 查看热点状态

一旦创建热点后，您可以通过运行来验证其状态：

```bash
nmcli 连接显示
```

您应该看到活跃连接下的热点列表。

## 配置 IP 转发中

要通过热点共享您的互联网连接，您需要启用 IP 转发：

1. **启用 IP 转发**：

   ```bash
   sudo sysctl net.ipv4.ip_forward=1
   ```

2. **通过编辑 `/etc/sysctl.d/99-sysctl.conf` 使其成为永久**

   ```bash
   sudo nano /etc/sysctl.d/99-sysctl.conf
   ```

   增加以下行：

   ```
   net.ipv4.ip_forward=1
   ```

## 🛑 停止热点

要停止热点，只需运行：

```bash
热点下的 nmcli 连接
```
