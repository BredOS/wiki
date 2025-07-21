---
title: Pipewire CPU 正常工作
description:
published: true
date: 2025-03-16T16：17：09.241Z
tags:
editor: markdown
dateCreated: 2025-03-16T16：17：09.241Z
---

# Pipewire CPU 使用情况

管道不再吃你的核心之一吗？

好吧，你现在能做的最好就是只限制它使用 `systemd` 。

### 步骤 1：

创建文件 "~/.config/systemd/user/pipewire.service" 并将以下数据放置在它之内：

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

### 步骤 2：

保存文件并运行： `systemctl --user daemon-reload`

### 步骤 3：

登出或重新启动。 Pipewire 最多只能使用单个核心的10%。 **不要手动重启 pipewire 。**

这个哈克不应影响您的音频。
如果你想让它有更多的回旋余地, 更改行`CPUQuota`的百分比。