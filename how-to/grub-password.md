---
title: GRUB Password
description: Securing GRUB with a password
published: true
date: 2025-05-05T17:13:59.940Z
tags: 
editor: markdown
dateCreated: 2025-05-05T17:13:14.153Z
---

# 🔐 GRUB Password Protection

BredOS includes a utility to restrict GRUB boot options with a password.
This prevents unauthorized users from booting non-default entries or editing boot parameters.

# 🟢 Enable GRUB Password

`sudo grub-password`

You’ll be prompted to enter and confirm a password.
Once set, only the default GRUB entry can be booted without authentication.

# 🔴 Disable GRUB Password

`sudo grub-password -d`

This removes the password restriction and restores normal GRUB behavior.

## Notes

The configuration is stored in /etc/grub.d/99-bredos-grub-password.
The script regenerates GRUB config automatically via grub-mkconfig.