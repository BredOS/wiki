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
这将防止未经授权的用户启动非默认条目或编辑引导参数。

# 🟢 启用 GRUB 密码

`sudo grub-password`

您将被提示输入并确认密码。
一旦设置，只能在没有认证的情况下启动默认的 GRUB条目。

# 🔴 禁用 GRUB 密码

`sudo grub-password -d`

这将删除密码限制并恢复正常的 GRUB行为。

## 注

配置保存在/etc/grub.d/99-bredos-grub-密码中。
脚本通过 grub-mkconfig自动重新生成 GRUB配置。