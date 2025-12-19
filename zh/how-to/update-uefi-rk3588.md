---
title: 如何在 RK3588 上更新 UEFI
description: 学习如何更新基于RK3588的运行 BredOS 设备的 UEFI 固件
published: true
date: 2025-12-19T08:40:59.856Z
tags:
editor: markdown
dateCreated: 2025-02-23T15：28：48.131Z
---

# 1. 📥 安装固件

- 基于RK3588的设备的 UEFI 固件可以通过软件包管理器安装。 要为您的特定设备找到正确的软件包，请运行： 要为您的特定设备找到正确的软件包，请运行：

```
sudo pacman -Ss uefi
```

这将列出所有可用的 UEFI 固件包。 从列表中识别正确的设备包。 例如： 从列表中识别正确的设备包。 例如：

- **适用于 Edge2:** `edge2-uefi`
- **For FydetabDuo:** `fydetab-duo-uefi`
- **For Orange Pi 5:** `orangepi-5-uefi`
- **适用于 Rock 5B:** `rock-5b-uefi`
- (和产出中列出的其它内容)\*

# 2. 🛠️ 刷新UEFI 固件

- 一旦您为您的设备找到了正确的软件包，请使用以下方式安装：

```
sudo pacman -S <device-uefi-package>
```

- 例如，如果您正在使用 **FydetabDuo**，请运行：

```
sudo pacman -S fydetab-duo-uefi
```

# 3. 🔄 更新RK3588 设备上的 UEFI

安装后，固件图像将位于`/usr/shar/edk2/<device-name>/`。 系统将提供用于刷入固件的特定命令。\
命令的一般格式是：

> 系统将提供用于刷入固件的特定命令。 使用它而不是下面的 **通用** 格式！
> {.is-warning}

- 命令的 **general** 格式是：

### Tabset {.tabset}

#### eMMC

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/mmcblk0 bs=512 skip=64 seek=64 conv=notrunc
```

#### SD 卡

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/mmcblk1 bs=512 skip=64 seek=64 conv=notrunc
```

#### SPI 闪光灯

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/mtd0
```

###

例如，如果你在 **FydetabDuo** 上使用 **eMMC 存储** ，命令将是：

```
sudo dd if=/usr/share/edk2/fydetab-duo/fydetab-duo_UEFI_Release_v0.12.3.img of=/dev/mmcblk0 bs=512 skip=64 search=64 conv=notrunc
```

> **Done!** Your device's UEFI firmware is now updated.
> {.is-success}

