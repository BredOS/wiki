---
title: Pipewire CPU 回避策
description:
published: true
date: 2025-03-16T16:17:09.241Z
tags:
editor: markdown
dateCreated: 2025-03-16T16:17:09.241Z
---

# Pipewire CPU使用率を回避する

パイプワイヤーは再び理由なしであなたのコアの一つを食べていますか?

今できることは、 `systemd` での使用を制限することです。

### ステップ 1:

`~/.config/systemd/user/pipewire.service` ファイルを作成し、以下のデータを保存します。

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

### ステップ 2:

ファイルを保存して実行: `systemctl --user daemon-reload`

### ステップ 3:

ログアウトまたは理想的に再起動します。 パイプワイヤーは、最大で単一コアの10%のみを使用します。 **手動でパイプワイヤーを再起動しないでください。**

このハックはあなたのオーディオには影響しません。
もう少し余裕を持たせたい場合は、`CPUQuota`の行でパーセンテージを変更します。