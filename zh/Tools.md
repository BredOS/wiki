---
title: BredOS 工具
description: BredOS 提供的实用程序和工具
published: true
date: 2025-05-07T18:31:34.455Z
tags:
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# 1. 介绍信息

这将作为`breddos-tools`，与任何系统架构兼容，发送到`BredOS-any`存储库中。
它是BredOS的组成部分。 “bredos-tools”应默认安装。
它是BredOS的组成部分。 “bredos-tools”应默认安装。
它是BredOS的组成部分。 “bredos-tools”应默认安装。

- 如果不安装它：

```
sudo pacman -S bredos-tools
```

这个软件包包含大量工具，其唯一目的是简化 BredOS 的开发、维护和一般使用。

# 2. GRUB 密码保护

BredOS 包含一个用密码限制 GRUB 启动选项的实用程序。
这将防止未经授权的用户启动非默认条目或编辑启动参数。
这将防止未经授权的用户启动非默认条目或编辑引导参数。

## 🟢 启用 GRUB 密码

- 要启用 grub 密码保护，请执行：

```
sudo grub-password
```

您将被提示输入并确认密码。
您将被提示输入并确认密码。
一旦设置，只能在没有认证的情况下启动默认的 GRUB 条目。

## 🔴 禁用 GRUB 密码

- 🔐 GRUB 密码保护

```
sudo grub-password -d
```

这将删除密码限制并恢复正常的 GRUB 行为。

> 配置保存在 `/etc/grub.d/99-bredos-grub-password` 中。
> 脚本通过 `grub-mkconfig` 自动重新生成 GRUB 配置。
> 修改 `/etc/grub.d/10_linux`，请不要手动恢复。
> 配置保存在/etc/grub.d/99-bredos-grub-密码中。
> 脚本通过 grub-mkconfig自动重新生成 GRUB配置。
> 修改`/etc/grub.d/10_linux`，请不要手动恢复。
> 配置保存在 `/etc/grub.d/99-bredos-grub-password` 中。
> 脚本通过 `grub-mkconfig` 自动重新生成 GRUB 配置。
> 修改 `/etc/grub.d/10_linux`，请不要手动恢复。
> 配置保存在/etc/grub.d/99-bredos-grub-密码中。
> 脚本通过 grub-mkconfig自动重新生成 GRUB配置。
> 修改`/etc/grub.d/10_linux`，请不要手动恢复。
> 配置保存在 `/etc/grub.d/99-bredos-grub-password` 中。
> 脚本通过 `grub-mkconfig` 自动重新生成 GRUB 配置。
> 修改 `/etc/grub.d/10_linux`，请不要手动恢复。
> 配置保存在/etc/grub.d/99-bredos-grub-密码中。
> 脚本通过 grub-mkconfig自动重新生成 GRUB配置。
> 修改`/etc/grub.d/10_linux`，请不要手动恢复。
> 这修改了 `/etc/grub.d/10_linux` ，不要手动还原它！
> {.is-info}
> {.is-info}
> {.is-info}

# 3. DTSC 助手脚本

- 要使它起作用，你需要安装 `dtc`，只需运行 `yay -S dtc`

```
yay -S dtc
```

脚本是一个 dtc 的包装器，执行自动的 gcc 预处理、链接和生成所需文件。
它使得设备树的生成和测试大为简化。
它自动决定并生成基础设备树或叠加层。
它使得设备树的生成和测试大为简化。
它还自动决定并生成基础设备树或叠加层。

> 在您的设备上安装不正确的设备树将使它无法操作。
> 小心，执行备份并确保一个紧急计划。
> {.is-warning}
> 小心，执行备份并确保一个紧急计划。
> {.is-warning}
> 小心，执行备份并确保一个紧急计划。
> {.is-warning}

## 3.1 用法

- 用参数 "-h" 运行 dtsc 以显示其用法：

```
用法：dtsc [-h] [-o OUTPUT] [-i INCLUDE] [-k KERNEL] [input]

将一个设备树源(DTS) 文件编译成一个设备树二进制文件(DTBO 或 DTB)。

位置参数：
  input                 输入 DTS 文件

选项：
  -h, --help            显示此帮助消息并退出
  -o, --output OUTPUT   输出文件(默认：生成匹配输入文件名的 .dtb)
  -i, --include INCLUDE 附加设备树文件(可选)
  -k, --kernel KERNEL   手动指定内核源路径 (默认：自动检测)

示例：dtsc my_device_tree.dts -o output.dtbo
```

## 输入

脚本需要输入 `.dts` 文件。如果没有指定输出，它生成匹配名称的 `.dtb` 文件。
输出文件名可以用 `-o` 参数设置。 脚本需要输入 `.dts` 文件。如果没有指定输出，它生成匹配名称的 `.dtb` 文件。
输出文件名可以用 `-o` 参数设置。 如果没有指定输出, 它生成了匹配名称`.dtb`
输出文件名可以设置为 `-o` 参数。

## 3.3 与内核关联

如果您有多个内核安装在您的系统上，您应该指定要链接的内核路径。
它应该看起来像这样：

- 它应该看起来像这样：

```
dtsc example.dts -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

如果您安装了单个内核，这将自动被检测。

## 编译基础设备树

如果您正在编译基础设备树而不是叠加层，您将需要您的内核全部源码，这些源码没有预装。
这是因为这些树需要包含其他 ".dtsi" 设备树。
这是因为这些树需要包含其他 ".dtsi" 设备树。

要编译这样一个设备树，请使用 git 克隆你的内核存储库到已知路径。

- `linux-rockchip-rkr3` 内核的示例：

```
git clone https://github.com/BredOS/linux-bredos
```

然后按您想要的方式运行 dtsc，但使用 "-i" 标志指定它想要链接的文件夹。

- 例如，假定我们想要编译一个 rk3588 开发板的设备树，我们需要指定以下选项：

```
dtsc rk3588-exampleboard.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-exampleboard.dtb
```