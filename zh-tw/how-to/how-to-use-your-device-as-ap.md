---
title: How to use your device as a wireless hotspot
description:
published: true
date: 2025-09-16T10:50:45.422Z
tags:
editor: markdown
dateCreated: 2024-09-08T10:33:46.772Z
---

# 1. 🛠️ Prerequisites

This guide will show you how to set up a Wi-Fi hotspot using NetworkManager.

# 3. View Hotspot Status

Before you begin, make sure you have:

- 📡 A Wi-Fi adapter that supports AP (Access Point) mode

> Suitable devices that support AP (Access Point) mode include Rock 5C, Rock 5B+, Khadas Edge 2, Khadas Vim 4, all Mekotronics R58 devices, and the Orange Pi 5B.
> {.is-info}

# 4. Configure IP Forwarding

## 2. Create a Hotspot

You can easily create a hotspot using the NetworkManager command-line tool `nmcli`.

- **List your network devices** to identify the Wi-Fi interface you’ll use:

```bash
nmcli device status
```

- Example output

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

- **Create the hotspot** by using the following command:

```bash
nmcli device wifi hotspot ifname <wifi_interface> ssid <MyHotspot> password <mypassword>
```

- Example output

```
Device 'wlan0' successfully activated with '4d090d70-fd85-45bc-bf36-a63846f3f805'. 
Hint: "nmcli dev wifi show-password" shows the Wi-Fi name and password.
```

```
Replace `<wifi_interface>` with your actual interface name, like `wlp2s0` or `wlan0`,  `<MyHotspot>` with your desired SSID and `<mypassword>` with a secure passphrase of your choice.
```

> If you get the following error run the command again with sudo.
> If you get the following error run the command again with sudo
> `Error: Failed to setup a Wi-Fi hotspot: Not authorized to control networking.`
> {.is-info}

## 3.2 View Hotspot Status

- Once the hotspot is created, you can verify its status by running:

```bash
nmcli connection show
```

- Example output

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

You should see the hotspot listed under the active connections.

## 3.3 Configure IP Forwarding

To share your internet connection through the hotspot, you need to enable IP forwarding:

- **Enable IP forwarding**:

```bash
sudo sysctl net.ipv4.ip_forward=1
```

- **Make it permanent** by editing `/etc/sysctl.d/99-sysctl.conf`:

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
