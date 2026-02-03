---
title: 在 BredOS 上安装 STEAM (FEX-Emu)
description:
published: false
date: 2026-02-03T09:17:38.531Z
tags:
editor: markdown
dateCreated: 2026-01-27T09：08：49.245Z
---

# 2. 介绍信息

欢迎来到关于如何在 BredOS 上安装 **Steam** 的指南！ 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。 跟着这些简单的步骤来让Steam在您的系统上站起来。

> 这篇文章是为了基于ARMv9 System-on-Chip而设计的，如Cix Pi 81x0。 ARMv8 SOC支持执行32位代码。 对于ARMv8 SBC，请使用 [box64](/en/how-to/how-to-install-steam) 代替！
> {.is-info}

# 3. 安装FEX-Emu

## 2.1 安装 FEX 二进制文件

截至编写本报告时，您需要自己编译FEX-Emu。 我们准备了一个PKGBUILD文件来简化这一过程。

- 克隆我们的 FEX-仓库：

```
git clone https://github.com/BredOS/BredOS-FEX-Emu.git
```

- 要构建最新版本的 FEX，您需要修改PKGBUILD 文件：

```
cd BredOS-FEX-Emu/BredOS
nano PKGBUILD
```

- 文件看起来像这样：

```
pkgname=bredos-fex-emu
pkgver=2509.1
pkgrel=2
pkgdesc='快速用户模式 x86 和 x86-64 模拟器for Arm64 - BredOS Edition'
url=https://BredOS。 rg
arch=(aarch64)
license=(GPL3)

[等于...]
```

- 访问 https://github.com/FEX-Emu/FEX 并寻找一个有效的标签。 截至撰写本报告之时，最近一次释放是从2026年1月开始。 与此版本关联的标签是 2601。 相应编辑 pkgver\`

```
pkgver=2601
```

关闭并使用 <kbd>CTRL</kbd> + <kbd>X</kbd>, 然后 <kbd>Y</kbd>

- 使用 FEX 构建并安装 FEX

```
毫克-西文
```

## 2.2 安装 x86_64 根文件系统

为了简化一个 BredOS x86_64 根文件系统的安装，我们开发了我们自己的 `fex-config` 工具。

- 要获取rootfs，请运行：

```
sudo fex-config -c
```

这将下载并安装 BredOS 到 "~/.fex-emu/RooTFS/bredos-chroot"

# 4. Steam安装

## 3.1 启用多lib

您可能需要添加 **BredOS Multilib** 仓库来安装 Steam 和必要的翻译层。 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤： 要做到这一点，请遵循以下步骤：

- 安装 `bredos-mullib` 包

```
   sudo pacman -S bredos-multilib
```

- 运行时更新软件包数据库：

```
   sudo pacman -Sy
```

## 3.2 Steam安装

- 运行以下命令来安装 Steam：

```
   sudo pacman -Sdd steam
```

# 5. GPU 加速

## 4.1 英特尔和AMD

Intel 和 AMD 图形卡应该用盒子运行，只要您的主机系统启用了图形加速。

> 这只用AMD卡进行过测试。 如果您有英特尔卡，请随时在我们的 Discord 或 Telegram 频道分享您的体验。
> {.is-info}

## 4.2 NVidia

确保您已经在您的主机系统上安装了专有的 NVIDIA 驱动程序。 开源的 Nouveau 驱动程序将无法工作。 只要我们的 `fex-config` 工具能够检测到 NVIDIA 驱动程序，它就会自动为您安装x86_64 驱动程序。

> 请参阅 [here](https://github.com/MitchellAugustin/fex_autoinstall/blob/main/fex_autoinstall_poc.sh)，了解如何安装驱动程序。
> {.is-info}

## 4.3 任何其他GPU

如果您想要使用您单一看板电脑的内部图形卡，您需要启用导星。 Thunk图书馆充当翻译GPU呼叫的中介。

> 在 FEX-Emu 上启用小块使得FEX 极难稳定！
> {.is-info}

- 编辑 FEX的 Config.json

```
nano $HOME/.fex-emu/Config.json
```

- 定位配置文件中的Thunks部分：

```
  "ThunksDB": own
    "fex_thunk_test": 0,
    "asound": 0,
    "drm": 0,
    "Vulkan": 0,
    "WaylandClient": 0,
    "GL": 0
}
```

- 并编辑它以启用 `Vulkan`, `WaylandClient` 和 `GL`：

```
  "ThunksDB": own
    "fex_thunk_test": 0,
    "asound": 0,
    "drm": 0,
    "Vulkan": 1,
    "WaylandClient": 1,
    "GL": 1
}
```

# 4. 启动Steam

- 安装完成后，您可以通过在应用程序菜单中搜索或运行来启动Steam：

```
steam
```

> 快乐游戏！
> {.is-success}
> 快乐游戏！
> {.is-success}
> {.is-success}

# 6. Troubleshooting

## 6.1 Steam hangs on start

- If Steam does not start for you, but hangs at:

```
steam.sh[7285]: Running Steam on bredos rolling 64-bit
steam.sh[7285]: STEAM_RUNTIME is enabled by the user
setup.sh[7328]: Steam runtime environment up-to-date!
```

- Open a new Console and execute:

```
killall FEXServer
```

Steam will then continue to load normally.

\*[SBCs]: 单一板电脑
