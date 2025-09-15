---
title: How to use your device as a wireless hotspot
description:
published: true
date: 2025-09-15T09:43:47.485Z
tags:
editor: markdown
dateCreated: 2024-09-08T10:33:46.772Z
---

# 1. 簡介

This guide will show you how to set up a Wi-Fi hotspot using NetworkManager.

# 2. Prerequisites

Before you begin, make sure you have:

- A Wi-Fi adapter that supports AP (Access Point) mode

> Suitable devices that support AP (Access Point) mode include Rock 5C, Rock 5B+, Khadas Edge 2, Khadas Vim 4, all Mekotronics R58 devices, and the Orange Pi 5B.
> {.is-info}

# 3. 安裝

## 3.1 Create a Hotspot

You can easily create a hotspot using the NetworkManager command-line tool `nmcli`.

- List your network devices to identify the Wi-Fi interface you’ll use:

  ```bash
  nmcli device status
  ```

- Create the hotspot by using the following command:

  ```bash
  nmcli device wifi hotspot ifname <wifi_interface> ssid <MyHotspot> password <mypassword>
  ```

  Replace `<wifi_interface>` with your actual interface name, like `wlp2s0` or `wlan0`,  `<MyHotspot>` with your desired SSID and `<mypassword>` with a secure passphrase of your choice.

> If you get the following error run the command again with sudo
> `Error: Failed to setup a Wi-Fi hotspot: Not authorized to control networking.`
> {.is-info}

## 3.2 View Hotspot Status

- Once the hotspot is created, you can verify its status by running:

```bash
nmcli connection show
```

You should see the hotspot listed under the active connections.

## 3.3 Configure IP Forwarding

To share your internet connection through the hotspot, you need to enable IP forwarding:

- Enable IP forwarding:

  ```bash
  sudo sysctl net.ipv4.ip_forward=1
  ```

- Make it permanent by editing `/etc/sysctl.d/99-sysctl.conf`:

  ```bash
  sudo nano /etc/sysctl.d/99-sysctl.conf
  ```

- Add the following line:

  ```
  net.ipv4.ip_forward=1
  ```

## 3.4 Stopping the Hotspot

- To stop the hotspot, simply run:

```bash
nmcli connection down Hotspot
```
