---
title: GRUB密码
description: 使用密码保护 GRUB
published: true
date: 2025-05-05T17:13:59.940Z
tags: null
editor: markdown
dateCreated: 2025-05-05T17：13：14.153Z
---

# 🔐 GRUB 密码保护

BredOS 包含一个用密码限制GRUB启动选项的工具。
This prevents unauthorized users from booting non-default entries or editing boot parameters.

# 🟢 启用 GRUB 密码

`sudo grub-password`

您将被提示输入并确认密码。
Once set, only the default GRUB entry can be booted without authentication.

# 🔴 Disable GRUB Password

`sudo grub-password -d`

This removes the password restriction and restores normal GRUB behavior.

## Notes

The configuration is stored in /etc/grub.d/99-bredos-grub-password.
The script regenerates GRUB config automatically via grub-mkconfig.