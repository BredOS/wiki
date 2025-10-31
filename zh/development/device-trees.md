---
title: 设备树
description:
published: true
date: 2025-05-15T12:51:43.781Z
tags:
editor: markdown
dateCreated: 2024-11T11:50:39.940Z
---

# 1. 简介

设备树是一种描述ARM和RISC-V系统通常使用的硬件的机制。 允许内核在不改变内核驱动程序代码的情况下发现和配置硬件设备。
与x86系统不同的是，ACPI表格使得自动硬件发现和配置成为可能。 大多数ARM 系统需要修改设备树才能声明硬件更改。
与x86系统不同的是，ACPI表格使得自动硬件发现和配置成为可能。 大多数ARM 系统需要修改设备树才能声明硬件更改。

# 2. 设备树

## 在 UEFI 和 Grub 系统中切换设备树

打开 grub 配置文件 `/etc/default/grub` 。
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：

- 打开 grub 配置文件 `/etc/default/grub` 。
  找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```

- 然后更新grub 配置：

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

> 只能指定一个 DTB
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

## Updating Device Trees in U-Boot systems with extlinux

- 编辑 extlinux 配置文件 `/boot/extlinux/extlinux.conf` 。 使用 fdt\`, 例如: 使用 fdt`, 例如: 使用 fdt\`, 例如: 使用 fdt`, 例如:

```bash
fdt /dtbs/rockchip/xxx.dtb
```

然后编辑以匹配您的设备树路径。 保存并重启您的系统。 保存并重启您的系统。 保存并重启您的系统。 保存并重启您的系统。

> 只能指定一个 DTB
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
