---
title: 🧹💾 Disk Space Cleanup Guide
description: BredOS Disk Space Cleanup Guide 🧹💾
published: true
date: 2025-09-16T10:42:55.802Z
tags:
editor: markdown
dateCreated: 2024-09-20T20:26:57.698Z
---

# 1. 簡介

Over time, your system may accumulate unnecessary files that take up valuable space. This guide will walk you through several methods to reclaim disk space on your BredOS system.

# 2. Clean Package Cache 📦

When installing or updating packages, **Pacman** keeps cached copies in `/var/cache/pacman/pkg/` to make reinstallation faster. However, these cached packages can accumulate and use up disk space.

## Check Cache Size 📏

- To see how big the package cache is, run:

```
du -sh /var/cache/pacman/pkg/
```

## Manual Cleanup 🗑️

- You can manually remove cached packages that are no longer installed with:

```
sudo pacman -Sc
```

## Automatic Cleanup with Paccache 🔄

You can also use `paccache` to keep only the most recent 3 versions of each package:

- Install the required tool:

```
sudo pacman -S pacman-contrib
```

- Set up a Pacman hook to automatically clean up after each transaction:

```
sudo nano /usr/share/libalpm/hooks/paccache.hook
```

- Add the following content to the file:

```
[Trigger]
Operation = Upgrade
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
Description = Cleaning pacman cache with paccache…
When = PostTransaction
Exec = /usr/bin/paccache -r
```

- Save the file with **Ctrl + S** and exit with **Ctrl + X**.

# 3. Clean Old Log Files 📝

- System logs can take up a considerable amount of space over time. You can check the size of your logs with:

```bash
journalctl --disk-usage
```

## Clean Up Old Logs 🧼

- To remove logs older than 3 days:

```bash
sudo journalctl --vacuum-time=3d
```

# 4. Use BleachBit 🧽

**BleachBit** is a powerful tool that helps you clean up system junk, free disk space, and protect your privacy. You can learn more about how to use BleachBit [here](https://www.bleachbit.org/).

# 5. Clean User Cache 🏠

- As you use your system, caches will accumulate in your home directory. You can check the size of your cache folder with:

```bash
sudo du -sh ~/.cache/
```

## Clean the Cache 🧹

- To remove all cache files:

```bash
rm -rf ~/.cache/*
```

---

# 5. Find Large Files and Directories 📂

Sometimes, large files can take up space unnecessarily. Here are tools you can use to identify them:

## Console Tools ⌨️

- **duc** — A disk usage inspector.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`  
  **duc** — A disk usage inspector.\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`  
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- **gdu** — Disk usage analyzer with console interface.\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`  
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`  
  [GitHub](https://github.com/dundee/gdu) | AUR: `gduAUR`

- **ncdu** — ncurses disk usage analyzer.\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`  
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`  
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`

## Graphical Tools 🖼️

- **Filelight** — Interactive disk usage map with concentric rings.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  **Filelight** — Interactive disk usage map with concentric rings.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`  
  **Filelight** — Interactive disk usage map with concentric rings.\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`

- **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`  
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  **GNOME Disk Usage Analyzer (baobab)** — Disk usage analyzer for GNOME.\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) | AUR: `baobab`

- **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`  
  **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`  
  **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  **qdirstat** — Qt-based directory statistics tool.\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`

---

> Free up space and keep your BredOS system running smoothly!
> 💪✨

