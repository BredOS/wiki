---
title: Btrfs Snapshots and Rollbacks with Timeshift 
description: A comprehensive guide on setting up Btrfs snapshots and system rollbacks using Timeshift
published: true
date: 2025-09-18T07:42:00.324Z
tags: 
editor: markdown
dateCreated: 2024-09-27T19:19:08.209Z
---

# 1. Introduction  
The snapshot feature of the Btrfs filesystem can be used to perform system snapshots and rollbacks. Timeshift is a user-friendly graphical application that makes this process easy!


# 2. Boot into Timeshift Snapshots from GRUB

When properly configured, `grub-btrfs` allows you to boot into Timeshift Btrfs snapshots directly from the GRUB menu, making system rollbacks easy and quick.

## 2.1 Install grub-btrfs
- To install `grub-btrfs` run:
```
sudo pacman -S grub-btrfs
```
Once installed, every time the GRUB configuration file gets updated, GRUB boot entries for existing Timeshift Btrfs snapshots will automatically be created. 
- You can update the GRUB configuration with:
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 2.2 Automate GRUB Configuration Updates
`grub-btrfs` can automate the GRUB update process whenever a new Timeshift Btrfs snapshot is created.

- Run the following command to edit the grub-btrfs path unit:

   ```
   sudo systemctl edit --full grub-btrfs.path
   ```
   
- Replace the content with the following:
   ```
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

- This step is reversible if needed, using:
   ```
   sudo systemctl revert grub-btrfs.path
   ```

## 2.3 Enable Automatic GRUB Updates
- Activate the automatic update of the GRUB configuration file by running:
```
sudo systemctl enable --now grub-btrfs.path
```

- You can further configure grub-btrfs by editing the configuration file:
```
sudo nano /etc/default/grub-btrfs/config
```

---

# 3. Automatic System Snapshot with Timeshift-autosnap

You might want to install `timeshift-autosnap`, which automatically creates Timeshift snapshots before performing any package upgrades via Pacman. This ensures that you always have a restore point before changes are made to your system.

## 3.1 Install timeshift-autosnap
- To install `timeshift-autosnap` run:
```
sudo pacman -S timeshift-autosnap
```

## 3.2 Prevent Duplicate GRUB Updates
To avoid GRUB being updated twice when a snapshot is created by timeshift-autosnap, It's recommended to modify the configuration file. 
- Set `updateGrub` to `false` by editing the following file:
```
sudo nano /etc/timeshift-autosnap.conf
```

Change the line `updateGrub=true` to `updateGrub=false`.


> Having a robust snapshot system can save your day in case something goes wrong during an update or system change. 
{.is-success}

