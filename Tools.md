---
title: BredOS Tools
description: Utilities and Tools provided by BredOS
published: true
date: 2025-05-07T18:27:16.781Z
tags: 
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# BredOS Tools

Shipped as `bredos-tools`, compatible with any system architecture, on the `BredOS-any` repository.
An integral part of BredOS.

## Introductory info

This package contains a plethora of tools with the sole purpose of easing development, maintenance and the general use of BredOS.

BredOS doesn't ship preferences, it ships tools and functionality.

# 🔐 GRUB Password Protection

BredOS includes a utility to restrict GRUB boot options with a password.
This prevents unauthorized users from booting non-default entries or editing boot parameters.

### 🟢 Enable GRUB Password

```
sudo grub-password
```

You’ll be prompted to enter and confirm a password.
Once set, only the default GRUB entry can be booted without authentication.

### 🔴 Disable GRUB Password
```
sudo grub-password -d
```
This removes the password restriction and restores normal GRUB behavior.

### Notes

The configuration is stored in /etc/grub.d/99-bredos-grub-password.
The script regenerates GRUB config automatically via grub-mkconfig.
Modifies `/etc/grub.d/10_linux`, do not revert manually.