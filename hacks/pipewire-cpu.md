---
title: Pipewire CPU workaround
description: 
published: true
date: 2025-09-17T09:24:40.286Z
tags: 
editor: markdown
dateCreated: 2025-03-16T16:17:09.241Z
---

# 1. Introduction
Is pipewire eating one of your cores for no reason again?

Well, best you can do right now is to just limit it's usage with `systemd`.

# 2. Limit CPU Quota
## 2.1 Create service file:
- Create file `~/.config/systemd/user/pipewire.service` and place the following data inside it:
```
[Unit]
Description=PipeWire Multimedia Service

# We require pipewire.socket to be active before starting the daemon, because
# while it is possible to use the service without the socket, it is not clear
# why it would be desirable.
#
# A user installing pipewire and doing `systemctl --user start pipewire`
# will not get the socket started, which might be confusing and problematic if
# the server is to be restarted later on, as the client autospawn feature
# might kick in. Also, a start of the socket unit will fail, adding to the
# confusion.
#
# After=pipewire.socket is not needed, as it is already implicit in the
# socket-service relationship, see systemd.socket(5).
Requires=pipewire.socket

[Service]
CPUAccounting=true
CPUQuota=10%
LockPersonality=yes
MemoryDenyWriteExecute=yes
NoNewPrivileges=yes
RestrictNamespaces=yes
SystemCallArchitectures=native
SystemCallFilter=@system-service
Type=simple
ExecStart=/usr/bin/pipewire
Restart=on-failure
Slice=session.slice

[Install]
Also=pipewire.socket
WantedBy=default.target
```
## 2.2 Reload systemd daemon
- Save the file and run: 
```
systemctl --user daemon-reload
```

## 2.3 Logout or reboot:
Logout, or ideally reboot. Pipewire will only be using 10% of a single core at most. 
> Do not restart pipewire manually.
{.is-warning}


This hack should not affect your audio.
If you want to allow it some more leeway, change the percentage at line `CPUQuota`.