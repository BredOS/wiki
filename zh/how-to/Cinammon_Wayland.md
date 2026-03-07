---
title: Cinnamon Wayland 与 GPU 加速 RK3588
description: 用 RK3588 板上的硬件加速渲染从 X11 切换到Wayland
published: true
date: 2026-03-07T16：07：08.925Z
tags: 电影院, 航行, gpu, panthor, rk3588
editor: markdown
dateCreated: 2026-03-07T16：06：02.388Z
---

# 2. 介绍信息

Cinnamon 支持 Wayland 会话，从版本 `6.4`开始。 在 RK3588 板上 从 X11 切换到 Wayland 需要额外配置，因为SoC 会显示两个单独的 DRM 设备：一个用于显示输出, 一个用于GPU 渲染。 没有正确的设置，Cinnamon的合成器 (`Muffin`) 返回到`llvmpipe` 软件渲染，导致桌面性能不佳。

本指南通过开启完全GPU-加速的 Cinnamon Wayland 会话在BredOS上游。

# 3. 创建热点

## 2.1 所需软件包

- 验证所有必需的软件包已安装：

```
sudo pacman -S --need cinnamon muffin wayland xorg-xwayland libink pipewire mesa libdrm
```

## 2.2 内核和 GPU 驱动程序

- 验证 panthor\` 模块已加载：

```
lsmod | grep panthor
```

你应该在输出中看到了 panthor\`。 如果不是，手动加载：

- 加载模块：

```
sudo modprobe panthor
```

> Panthor 需要 BredOS 内核`6.12` 或更高版本。 如果模块不可用，请更新内核。
> {.is-info}

# 3. 理解双GPU设置

在 RK3588 板上，内核暴露了两个DRI 卡设备。 这是Cinnamon Wayland大多数GPU加速问题的根源。

- 下表显示每个设备的角色：

| 设备                       | 驱动程序           | 作用                                                               |
| ------------------------ | -------------- | ---------------------------------------------------------------- |
| `/dev/dri/card0`         | `rockchip-drm` | 显示控制器 (HDMI/DP 输出). 没有 3D 渲染。 |
| `/dev/dri/card1`         | `panthor`      | GPU (Mali-G610). 处理所有3D渲染。    |
| `/dev/dri/renderD128`    | `panthor`      | GPU 渲染节点(3D)                                  |
| {.dense} |                |                                                                  |

问题: `Muffin` (Cinnamon's compositor, a fork of GNOME's Mutter) 尝试使用 `card0` 作为默认渲染。 因为`rockchip-drm`没有3D功能，它回落到`llvmpipe`(CPU软件渲染)。

解决方法：告诉Muffin使用 panthor` 渲染节点以加速GPU ，同时保持`rockchip-drm\` 以显示输出。

- 验证您的设备布局：

```
ls -l /dev/dri/
```

- 检查每张卡背面的驱动程序：

```
udevadm info -q property -n /dev/dri/card0 | grep DRIVER
udevadm info -q property -n /dev/dri/card1 | grep DRIVER
```

# 5. 配置 GPU 选择

## 4.1 创建 Udev 规则

最可靠的方法是 `udev` 规则，它告诉Muffin 设备更喜欢渲染。

- 创建 udev 规则文件：

```
sudo nano /etc/udev/rules.d/61-mutter-mutpanthor.rules
```

- 增加以下内容：

```
# RK3588: 将Panthor 渲染节点标记为Mutter/Muffin
SUBSYSTEM=="drm", KERNEL=="card1", DRIVERS=="panthor", TAG+="mutter-device-heaved-primarary"
```

- 重新加载udev规则：

```
sudo udevadm control --reload
sudo udevadm trigger
```

- 验证标签是否已应用：

```
udevadm info -q all -n /dev/dri/card1 | grep mutter
```

你应该在输出中看到`mutter-device-chered-primary`。

## 4.2 设置环境变量

除了udev规则外，设置环境变量，帮助Muffin和Mesa选择正确的 GPU。

- 创建环境配置文件：

```
sudo nano /etc/environment.d/90-rk3588-gpu.conf
```

- 增加以下内容：

```
# Mutter/Muffin Wayland
MUTTER_ALLOW_HYBRID_GPUS=1
```

> 不设置 `WLR_DRM_DEVICES` - 变量适用于wlroot-based composator(Sway, Hyprland)，而不适用于Muffin。 设置它对 Cinnamon 没有影响。
> {.is-info}

## 4.3 删除不正确的配置

如果你先前创建了一个 `/etc/environment.d/gpu-wayland.conf` 等变量，如`WLR_DRM_DEVICES`, `MESA_LOADER_DRIVER_OVERRIDE`, 或 `MUTTER_DEBUG_FORCE_EGL_STREAM`, 移除或重命名它。 这些变量不适用于Muffin，可能导致意外行为。

- 检查旧配置：

```
ls /etc/environment.d/
```

- 删除任何不正确的文件：

```
sudo rm /etc/environment.d/gpu-wayland.conf
```

# 4. 选择航道会话

## 5.1 来自登录屏幕

大多数显示管理器 (LightDM, GDM 允许从登录屏幕中选择会话类型。

- 在登录屏幕上寻找一个装备图标或会话选择器
- 选择 `Cinnamon (Wayland)` 而不是 `Cinnamon`
- 正常登录

## 5.2 验证会话类型

登录后：

- 确认您正在运行一个航道会话：

```
echo $XDG_SESSION_TYPE
```

产出应为“wayland”。

# 🔄 3. 验证 GPU 加速

## 6.1 检查渲染器

在Wayland，您必须使用 `eglinfo` 来检查GPU 加速。 `glxinfo`命令穿过XWayland 并且可能不正确地显示`llvmpipe`，即使合成器加速GPU。

- 安装`eglinfo` 如果不存在：

```
sudo pacman -S --needmesa-utils
```

- 检查EGL 渲染器：

```
eglinfo -B 2>/dev/null | grep -A2 "设备平台"
```

你应该在输出中看到`Mali-G610`或`panthor`，而不是`llvmpipe`。

- 或者，检查Muffin在其日志中的报告：

```
journalctl --user -b -u cinnamon-session | grep -i "render\|gpu\|egl\|drm"
```

## 6.2 检查合成状态

- 打开 Cinnamon的系统设置，导航到 `General` 并检查是否启用 `Compositing`
- 或者，从终端中检查：

```
dconf read /org/cinnamon/muffin/compositing-manager
```

输出应为“true”。

# 9. 🤝 贡献

## 7.1 glxinfo Still Shows llvmpipe

预期在韦兰会有这种情况。 `glxinfo`命令使用通过 XWayland 的 GLX 协议。 即使有完全GPU-加速的Wayland会话，`glxinfo`也可能会报告`llvmpipe`，因为XWayland可能无法访问 GPU 渲染节点。

- Use `eglinfo` instead to verify the Wayland renderer (see [section 6.1](#h-61-check-the-renderer))
- 要修复在 XWayland 下运行的 X11 应用程序的 "glxinfo" ，请尝试：

```
DRI_PRIME=1 glxinfo -B
```

## 7.2 Cinnamon Falls回到软件渲染中

如果`eglinfo`也显示`llvmpipe`：

- 验证 udev 规则已经应用(见[第4.1节] (#h-41-create-a-udev-rule))
- 检查您的 Mesa 版本是否支持Panthor (`mesa >= 24.1`)
- 请确保未安装供应商 `libMali` ，因为它与Mesa冲突：

```
pacman -Q | grep -i mali
```

如果发现任何`libmali`软件包，请删除它：

- 删除冲突包：

```
sudo pacman -R libmali-valhall-g610
```

- 查看 Muffin的日志错误：

```
journalctl --user -b | grep -i muffin
```

## 7.3 黑屏或登录循环

如果Wayland会话未能开始：

- 使用 `Ctrl+Alt+F2` 切换到TTY 并登录
- 检查会话日志：

```
journalctl --user -b -u cinnamon-session
```

- 作为一个工作区，从登录界面回到X11会话并验证您的配置

## 7.4 屏幕窃听或性能差

如果会话开始，但性能很差：

- Verify compositing is enabled (see [section 6.2](#h-62-check-compositing-status))
- 检查系统会话是否覆盖了 Flatpak 或 Snap 版本
- 如果你看到渲染伪影，请尝试将 `CLUTTER_PAINT=disable-culling` 添加到 `/etc/environment.d/90-rk3588-gpu.conf`

## 7.5 还原到 X11

如果Wayland工作不正确， 您总是可以通过选择 `Cinnamon` 会话切换回X11 (没有"航行"标签)。

# 4. Summary

- 下表汇总了所需的变化：

| 什么                       | 文件                                          | 内容                           |
| ------------------------ | ------------------------------------------- | ---------------------------- |
| Udev 规则                  | `/etc/udev/rules.d/61-mutter-Panthor.rules` | 标记`card1`为`突变设备-首选原始`        |
| 环境                       | `/etc/environment.d/90-rk3588-gpu.conf`     | `MUTTER_ALLOW_HYBRID_GPUS=1` |
| 会议                       | 登录屏幕                                        | 选择 `Cinnamon (Wayland)`      |
| {.dense} |                                             |                              |

# 10. 参考

- [Muffin 源代码](https://github.com/linuxmint/muffin) - Linux Mint
- [完全多GPU支持](https://gitlab.gnome.org/GNOME/mutter) - GNOME
- [Mesa Panthor driver](https://docs.mesa3d.org/drivers/panthor.html) - Mesa
- [Armbian RK3588 GPU 加速讨论](https://forum.armbian.com/topic/56374-expected-default-graphics-acceleration-for-rk3588/) - Armbian Forum