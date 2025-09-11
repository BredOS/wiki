---
title: 🧹💾 磁盘空间清理指南
description: 本指南将带着您几种方法来恢复您的 BredOS 系统上的磁盘空间。 🖥️✨ 🖥️✨ 🖥️✨
published: true
date: 2024-09-21T09:03:53.416Z
tags:
editor: markdown
dateCreated: 2024-09-20T20：26：57.698Z
---

# BredOS 磁盘空间清理指南 🧹💾

随着时间的推移，您的系统可能会积累不必要的文件，占用宝贵的空间。 随着时间的推移，您的系统可能会积累不必要的文件，占用宝贵的空间。 随着时间的推移，您的系统可能会积累不必要的文件，占用宝贵的空间。 本指南将带着您几种方法来恢复您的 BredOS 系统上的磁盘空间。 🖥️✨ 🖥️✨ 🖥️✨

---

## 📚 目录

- 清除软件包缓存 📦
- 清理旧日志文件 📝
- 使用 BleachBit 🧽
- 清理用户缓存 🏠
- 查找大文件和目录 📂

---

## 清除软件包缓存 📦

安装或更新软件包时，**Pacman** 将缓存的副本保存在`/var/cache/pacman/pkg/`中，以加快重新安装速度。 然而，这些缓存的软件包可以积累和使用磁盘空间。 然而，这些缓存的软件包可以积累和使用磁盘空间。 然而，这些缓存的软件包可以积累和使用磁盘空间。

### 检查缓存大小:简单的规则：

要查看软件包缓存的大度，请运行：

```bash
du -sh /var/cache/pacman/pkg/
```

### 手动清理 :waste篮子：

您可以手动移除已不再安装的缓存软件包：

```bash
sudo pacman -Sc
```

### 使用 Paccache :countrockwise_arrows_buton自动清理：

您也可以使用 **paccache** 来保留每个软件包最新的3个版本：

1. 安装所需工具：
   ```bash
   sudo pacman -S pacman-contrib
   ```
2. 设置一个 Pacman 钩子在每次交易后自动清理：
   ```bash
   sudo nano /usr/share/libalpm/hooks/paccache.hook
   ```
   在文件中添加以下内容：
   ```bash
   [Trigger]
   操作=升级
   操作=安装
   操作=删除
   类型=包
   目标=*

   [Action]
   描述=清理带paccache…
   当=PostTransaction
   Exec = /usr/bin/paccache -r
   ```
   将文件保存为 **Ctrl + S** 并以 **Ctrl + X** 退出

---

## 清理旧日志文件 📝

随着时间的推移，系统日志可能占用相当多的空间。 随着时间的推移，系统日志可能占用相当多的空间。 您可以通过以下方式检查您日志的大小： 随着时间的推移，系统日志可能占用相当多的空间。 您可以通过以下方式检查您日志的大小：

```bash
journalctl --disk-usage
```

### 清理旧日志 🧼

要删除3天以上的日志：

```bash
sudo journalctl --trainum-time=3d
```

---

## 使用 BleachBit 🧽

**BleachBit** 是一个强大的工具，可以帮助您清理系统垃圾，空闲磁盘空间，并保护您的隐私。 您可以了解更多关于如何使用 BleachBit [here](https://www.bleachbit.org/)。 您可以了解更多关于如何使用 BleachBit [here](https://www.bleachbit.org/)。 **BleachBit** 是一个强大的工具，可以帮助您清理系统垃圾，空闲磁盘空间，并保护您的隐私。 您可以了解更多关于如何使用 BleachBit [here](https://www.bleachbit.org/)。 您可以了解更多关于如何使用 BleachBit [here](https://www.bleachbit.org/)。 您可以了解更多关于如何使用 BleachBit [here](https://www.bleachbit.org/)。

---

## 清理用户缓存 🏠

当您使用您的系统时，缓存将会在您的主目录中累积。 您可以检查您的缓存文件夹大小： 手动清理 :waste篮子： 手动清理 :waste篮子：

```bash
sudo du -sh ~/.cache/
```

### 清理缓存 🧹

要移除所有缓存文件：

```bash
rm -rf ~/.cache/*
```

---

## 查找大文件和目录 📂

有时，大型文件可能不必要地占用空间。 以下是您可以用来识别他们的工具： 以下是您可以用来识别他们的工具： 以下是您可以用来识别他们的工具：

### 控制台工具 ⌨️

- **duc** - 磁盘使用情况检查器。\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- **gdu** - 控制台界面的磁盘使用情况分析器。\
  [GitHub](https://github.com/dunde/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dunde/gdu) | AUR: `gduAUR`\
  [GitHub](https://github.com/dunde/gdu) | AUR: `gduAUR`

- **ncdu** - ncurses 磁盘使用情况分析器。\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`\
  [Website](https://dev.yorhel.nl/ncdu) | AUR: `ncdu`

### 图形工具 🖼️

- **Filelight** - 具有聚合环的交互式磁盘使用图。\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  **Filelight** - 具有聚合环的交互式磁盘使用图。\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`\
  [Website](https://apps.kde.org/filelight) | AUR: `filelight`

- **GNOME 磁盘使用情况分析器(baobab)** - GNOME的磁盘使用情况分析器。\
  **GNOME 磁盘使用情况分析器(baobab)** - GNOME的磁盘使用情况分析器。\
  [Website](https://wiki.gnome.org/Apps/DiskUsageAnalyser) | AUR: `baobab`\
  **duc** - 磁盘使用情况检查器。\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`\
  [Website](https://duc.zevv.nl) | AUR: `ducAUR`

- 📚 目录\
  📚 目录\
  **qdirstat** - 基于Q的目录统计工具。\
  [GitHub](https://github.com/shundhammer/qdirstat) | AUR: `qdirstatAUR`

---

释放空间并保持您的 BredOS 系统的顺利运行！ 💪✨ 💪✨ 💪✨
