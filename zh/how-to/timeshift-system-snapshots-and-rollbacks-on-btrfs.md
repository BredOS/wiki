---
title: 使用 Timeshift 的 Btrfs 快照和回滚功能
description: 使用 Timeshift 设置Btrfs 快照和系统回滚的综合指南
published: true
date: 2025-09-18T07:42:00.324Z
tags:
editor: markdown
dateCreated: 2024-09-27T19：19：08.209Z
---

# 1. 简介

Btrfs 文件系统的快照功能可以用于执行系统快照和回滚。 时间跨度是一个方便用户的图形应用，方便了这个过程！

# 2. 从GRUB引导到时间快照

配置正确时，`grub-btrfs`可以让您直接从 GRUB菜单启动到 Timeshift Btrfs 快照，使系统回滚变得简单快捷。

## 2.1 安装 grub-Btrfs

- 安装 `grub-btrfs` 运行：

```
sudo pacman -S grub-btrfs
```

一旦安装完毕，每次更新 GRUB 配置文件时，将自动创建 GRUB 引导条目，用于现有的 Timeshift Btrfs 快照。

- 您可以更新GRUB配置：

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 2.2 GRUB 配置自动更新

`grub-btrfs` 可以在创建新的 Timeshift Btrfs 快照时实现GRUB更新过程的自动化。

- 运行以下命令来编辑 grub-Btrfs 路径单位：

  ```
  sudo systemctl 编辑 --full grub-btrfs.path
  ```

- 以下文取代内容：
  ```
  [Unit]
  Description=Monitors for new snapshots
  DefaultDependencies=no
  Requireres=run-timeshift-backup.mount
  After=run-timeshift-backup.mount
  BindsTo=run-timeshift-backup.mount

  [Path]
  PathModified=/run/timeshift/backup/timeshift-btrfs/snapshots

  [Install]
  WantedBy=run-titimeshift-backup.mount
  ```

- 如果需要，这个步骤是可逆的，使用：
  ```
  sudo systemctl return grub-btrfs.path
  ```

## 2.3 启用自动GRUB更新

- 运行 GRUB 配置文件的自动更新：

```
sudo systemctl 启用 --now grub-btrfs.path
```

- 您可以通过编辑配置文件来进一步配置 grub-Btrfs：

```
sudo nano /etc/default/grub-btrfs/config
```

---

# 3. 自动系统快照

您可能想要安装 `timeshift-autosnap` ，在通过 Pacman 进行任何软件包升级之前自动创建时间快照。 这将确保您在系统更改之前总是有一个恢复点。

## 3.1 安装时间间隔-自动osnap

- 要安装 `timeshift-autosnap` 运行：

```
sudo pacman -S timeshift-autosnap
```

## 3.2 防止重复 GRUB 更新

为了避免在 Timeshift-autosnapp 创建时两次更新 GRUB，建议修改配置文件。

- 通过编辑以下文件将 `updateGrub` 设置为 `false` ：

```
sudo nano /etc/timeshift-autosnap.conf
```

将“updateGrub=true”改为“updateGrub=false”。

> 拥有一个强大的快照系统可以在更新或系统更改过程中发生错误时节省您的日子。
> {.is-success}

