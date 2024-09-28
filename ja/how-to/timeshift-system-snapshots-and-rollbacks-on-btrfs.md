---
title: 📸🔄 Btrfs スナップショットとタイムシフトによるロールバック。
description: Timeshift スナップショットとシステムロールバックのセットアップに関する包括的なガイド
published: true
date: 2024-09-28T07:58:11.350Z
tags: null
editor: markdown
dateCreated: 2024-09-27T19:19:08.209Z
---

# 📸🔄 Btrfs スナップショットとタイムシフトによるロールバック。

**はじめに**\
**Btrfsファイルシステム**の**スナップショット機能**は、システムのスナップショットやロールバックを実行するために使用できます。 **Timeshift** is a user-friendly graphical application that makes this process easy!

---

# Boot into Timeshift Snapshots from GRUB with grub-btrfs 🚀

適切に設定されている場合、 **grub-btrfs** は、 **Timeshift** BtrfsスナップショットをGRUBメニューから直接起動することができ、システムのロールバックが簡単かつ迅速に行えます。

## Step 1: Install grub-btrfs 📦

To install **grub-btrfs**, run:

```bash
sudo pacman -S grub-btrfs
```

Once installed, every time the **GRUB** configuration file gets updated, GRUB boot entries for existing Timeshift Btrfs snapshots will automatically be created. You can update the GRUB configuration with:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Step 2: Automate GRUB Configuration Updates ⚙️

Grub-btrfs can automate the GRUB update process whenever a new **Timeshift Btrfs snapshot** is created.

1. Run the following command to edit the grub-btrfs path unit:
   ```bash
   sudo systemctl edit --full grub-btrfs.path
   ```

2. Replace the content with the following:
   ```bash
   [Unit]
   Description=Monitors for new snapshots
   DefaultDependencies=no
   Requires=run-timeshift-backup.mount
   After=run-timeshift-backup.mount
   BindsTo=run-timeshift-backup.mount

   [Path]
   PathModified=/run/timeshift/backup/timeshift-btrfs/snapshots

   [Install]
   WantedBy=run-timeshift-backup.mount
   ```

3. This step is **reversible** if needed, using:
   ```bash
   systemctl revert grub-btrfs.path
   ```

## Step 3: Enable Automatic GRUB Updates 🟢

Activate the automatic update of the GRUB configuration file by running:

```bash
sudo systemctl enable --now grub-btrfs.path
```

You can further configure grub-btrfs by editing the file located at:

```bash
/etc/default/grub-btrfs/config
```

---

# Automatic System Snapshot Before Package Upgrades with Timeshift-autosnap ⏳

You might want to install **timeshift-autosnap**, which automatically creates Timeshift snapshots before performing any package upgrades via Pacman. This ensures that you always have a **restore point** before changes are made to your system. 🛡️

## Step 1: Install timeshift-autosnap 📦

To install **timeshift-autosnap**, run:

```bash
sudo pacman -S timeshift-autosnap
```

## Step 2: Prevent Duplicate GRUB Updates ❌🔄

To avoid GRUB being updated twice when a snapshot is created by timeshift-autosnap, I recommend modifying the configuration file. Set `updateGrub` to `false` by editing the following file:

```bash
sudo nano /etc/timeshift-autosnap.conf
```

Change the line:

```bash
updateGrub=true
```

宛先:

```bash
updateGrub=false
```

---

このガイドが、Timeshiftで**Btrfsシステムスナップショット**と**ロールバック**のセットアップに役立つことを願っています！ 😊🔧 アップデートやシステムの変更中に問題が発生した場合に備えて、堅牢なスナップショットシステムを使用することで、一日を節約できます。 ハッピーコンピューティング！ 🖥️✨
