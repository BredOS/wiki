---
title: 蓝牙修复 (ITX-3588J)
description:
published: true
date: 2025-09-17T08：30：12.200Z
tags:
editor: markdown
dateCreated: 2025-09-14T11:10:38.109Z
---

# 1. 安装 r58x-postinstall

现在你必须用另一个软件包替换一个软件包。 这不会改变itx-3588j 的任何行为，但会添加一个将在启动时修复蓝牙的服务。

- 首先删除 itx-3588j-post-install\`。 这个软件包设置了一个围绕待命问题工作的必要参数。 我们不会再解决这个问题。

```
sudo pacman -R itx-3588j-post-install
```

- 然后，安装 `r58x-post-install`。 这个一揽子方案为上述待命状态提供了同样的解决办法，并包括了服务蓝牙计量仪。

```
sudo pacman -S r58x-post-install
```

# 2. 设置正确的 UART 路径

蓝牙适配器没有连接到 `/dev/ttyS9` (如它与其他 RK3588单板计算机一样)，而是连接到 `/dev/ttyS6` 。

- 您需要修改文件 /usr/bin/blutooth-fix的路径。

```
sudo nano /usr/bin/bluotooth-fix
```

```
#！/bin/bash

/usr/sbin/rfkill block 0
/usr/sbin/rfkill block blue bluetooth
/bin/sleep 2
/usr/sbin/rfkill unblock blue 0
/usr/sbin/rfkill unblock bluetooth

# FIXME 延迟
/bin/sleep 1

brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download--tosleep 200000 --baudrate 1500000 --patchram /libfirmware/ap6275 cd /dev/ttyS9
```

- 将最后一行改为 `/dev/ttyS6` 。

```
brcm_patchram_plus --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200 000 --baudrate 150 000 --patchram/lib/firmware/ap6275p/BCM4362A2.hcd /dev/ttyS6
```

# 3. 启用蓝牙服务

- 最终我们需要启用 `蓝牙-mekotronics` 服务

```
sudo systemctl --now 启用蓝牙-mekotronics
```

> 就是这样！ 就是这样！ 蓝牙现在应该正常工作。
> {.is-success}
> {.is-success}
