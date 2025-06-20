---
title: How to use your device as a wireless hotspot
description:
published: true
date: 2024-09-08T10:55:29.082Z
tags:
editor: markdown
dateCreated: 2024-09-08T10:33:46.772Z
---

# 📶 How to set up a hotspot using NetworkManager

This guide will show you how to set up a Wi-Fi hotspot using NetworkManager.

## 🛠️ Prerequisites

Before you begin, make sure you have:

- 📡 A Wi-Fi adapter that supports AP (Access Point) mode

> Suitable devices that support AP (Access Point) mode include Rock 5C, Rock 5B+, Khadas Edge 2, Khadas Vim 4, all Mekotronics R58 devices, and the Orange Pi 5B.
> {.is-info}

## Create a Hotspot

You can easily create a hotspot using the NetworkManager command-line tool `nmcli`.

1. **List your network devices** to identify the Wi-Fi interface you’ll use:

   ```bash
   nmcli device status
   ```

2. **Create the hotspot** by using the following command (replace `wifi_interface` with your actual interface name, like `wlp2s0` or `wlan0`):

   ```bash
   nmcli device wifi hotspot ifname wifi_interface ssid MyHotspot password "mypassword"
   ```

   This command will:

   - 📝 Create a hotspot with SSID `MyHotspot`
   - 🔑 Set the password to `mypassword`

> If you get the following error run the command again with sudo
> `Error: Failed to setup a Wi-Fi hotspot: Not authorized to control networking.`
> {.is-info}

## View Hotspot Status

Once the hotspot is created, you can verify its status by running:

```bash
nmcli connection show
```

You should see the hotspot listed under the active connections.

## Configure IP Forwarding

To share your internet connection through the hotspot, you need to enable IP forwarding:

1. **Enable IP forwarding**:

   ```bash
   sudo sysctl net.ipv4.ip_forward=1
   ```

2. **Make it permanent** by editing `/etc/sysctl.d/99-sysctl.conf`:

   ```bash
   sudo nano /etc/sysctl.d/99-sysctl.conf
   ```

   Add the following line:

   ```
   net.ipv4.ip_forward=1
   ```

## Stopping the Hotspot

To stop the hotspot, simply run:

```bash
nmcli connection down Hotspot
```
