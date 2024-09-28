---
title: "📸:countrockwise_arrows_buton: Btrfs Snapshots and Rollback, with Timeshift"
description: 使用 Timeshift 设置Btrfs 快照和系统回滚的综合指南
published: true
date: 2024-09-28T07：58：11.350Z
tags: null
editor: markdown
dateCreated: 2024-09-27T19：19：08.209Z
---

# 📸:countrockwise_arrows_buton: Btrfs Snapshots and Rollback, with Timeshift

**Introduction**\
**Btrfs 文件系统**的 **快照功能** 可以用于执行系统快照和回滚。 **Timeshift** 是一个方便用户的图形应用程序，方便此流程！

---

# 使用 grub-bfs :ro火箭从GRUB开启到Timeshift Snapshots

如果配置正确，**grub-btrfs** 允许您直接从 GRUB菜单启动到 \*\*Timeshift \*\* Btrfs 快照，使系统回滚变得简单快捷。

## 第 1 步：安装 grub-btrfs 📦

要安装 **grub-btrfs**，请运行：

```bash
sudo pacman -S grub-btrfs
```

一旦安装完毕，每次更新**GRUB** 配置文件时，将自动为 Timeshift Btrfs 创建GRUB启动条目。 您可以更新GRUB配置：

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 步骤 2: 自动更新 GRUB 配置 :gear：

当创建新 \*\*Timeshift Btrfs snapshot \*\* 时，Grub-Btrfs 可以实现GRUB更新过程自动化。

1. 运行以下命令来编辑 grub-Btrfs 路径单位：
   ```bash
   sudo systemctl 编辑 --full grub-btrfs.path
   ```

2. 以下文取代内容：
   ```bash
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

3. 如果需要，此步骤为 **可逆** ，使用：
   ```bash
   systemctl return grub-btrfs.path
   ```

## 第 3 步：启用自动GRUB 更新 :green_circle：

运行 GRUB 配置文件的自动更新：

```bash
sudo systemctl 启用 --now grub-btrfs.path
```

您可以通过编辑位于以下位置的文件来进一步配置 grub-Btrfs

```bash
/etc/default/grub-btrfs/config
```

---

# 软件包升级前自动系统快照，时间间隔为:小时glass_not_don：

您可能想要安装 **timeshift-autosnap**，在通过 Pacman 进行任何软件包升级之前自动创建 Timeshift 快照。 这确保您在系统更改之前总是有 **还原积分** 。 🛡️

## 第 1 步：安装时间间隔-自动osnap 📦

要安装 **timeshift-autosnap**，请运行：

```bash
sudo pacman -S timeshift-autosnap
```

## 步骤 2: 防止重复 GRUB 更新 ❌:countrockwise_arrows_buton:

为了避免在 Timeshift-autosnapp 创建时两次更新 GRUB，我建议修改配置文件。 通过编辑以下文件将 `updateGrub` 设置为 `false` ：

```bash
sudo nano /etc/timeshift-autosnap.conf
```

更改行：

```bash
updateGrub=true
```

至：

```bash
更新 Grub=false
```

---

我希望本指南已帮助您成功设置了 **Btrfs 系统快照** 和 **Rolbacks** 与 Timeshiff 成功！ :smiling_fac_with_smiling_eyes:🔧 拥有一个强大的快照系统可以在更新或系统更改时保存你的日子。 快乐的计算！ 🖥️✨
