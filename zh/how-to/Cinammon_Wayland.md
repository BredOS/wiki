---
title: Cinnamon Wayland 与 GPU 加速 RK3588
description: 用 RK3588 板上的硬件加速渲染从 X11 切换到Wayland
published: true
date: 2026-03-09T10:07:14.898Z
tags: 电影院, 航行, gpu, panthor, rk3588
editor: markdown
dateCreated: 2026-03-07T16：06：02.388Z
---

# 2. 介绍信息

Cinnamon 支持 Wayland 会话，从版本 `6.4`开始。 在 RK3588 板上 从 X11 切换到 Wayland 需要额外配置，因为SoC 会显示两个单独的 DRM 设备：一个用于显示输出, 一个用于GPU 渲染。 没有正确的设置，Cinnamon的合成器 (`Muffin`) 返回到`llvmpipe` 软件渲染，导致桌面性能不佳。

本指南通过开启完全GPU-加速的 Cinnamon Wayland 会话在BredOS上游。

> **已知限制 (Muffin 6.6.x)：** Muffin 尚不支持上游Mutter的 `mutter-device-chered-primarary` udev标签。 合成器本身正确使用 GPU 来构造桌面通过 GBM, 但Wayland EGL 客户端(GTK OpenGL 应用程序) 可能仍然会回到“llvmpipe”。 Vulkan 应用程序 (mpv, browsers, vkmark) 不受影响。 这一点已经在Rock 5B+ 和 Orange Pi 5 Plus上得到确认。 关于详细信息和工作情况，请参阅[第 7.8节](#h-78-wayland-egl-clients-use-llvmpipe-known-muffin-limitation节)。 其他Wayland作曲家(GNOME, KDE)在同一个硬件上正确处理多GPU。
> {.is-info}

# 3. 创建热点

## 2.1 所需软件包

- 验证所有必需的软件包已安装：

```
sudo pacman -S --need cinnamon muffin wayland xorg-xwayland libink pipewire mesa libdrm
```

## 2.2 内核和 GPU 驱动程序

本指南假设您已经启用了Panthor GPU驱动程序。 如果您仍在使用 Panfork (RK35xx) 的 BredOS 上默认值， 请先按照[安装马里的Panthor GPU with RK3588](/en/how-to/how-to-setup-panthor)指南，然后返回这里。

- 验证 panthor\` 模块已加载：

```
lsmod | grep panthor
```

你应该在输出中看到了 panthor\`。 如果不是，手动加载：

- 加载模块：

```
sudo modprobe panthor
```

> Panthor 需要 BredOS BSP 内核6.1-rkr3 或主线内核“6.12” 或更高版本。 如果模块不可用，请更新内核。
> {.is-info}

## 2.3 用户权限

您的用户必须属于“渲染”和“视频”组才能访问 GPU 渲染节点。 没有这些权限，应用程序就会静默地回到软件渲染上。

- 检查您当前的组：

```
组
```

如果输出缺少`render` 或 `video` ，请将您的用户添加到两个组：

```
sudo usermod -aG render,video $USER
```

**注销并重新登录以使群组更改生效。**

- 验证 GPU 渲染节点存在并可访问：

```
ls -la /dev/dri/
```

你应该至少看到`card0`、`card1`和`renderD128`。 `renderD128` 设备应该被`render` 组所拥有，并且必须有`crw-rw----`的权限。

> 如果`/dev/dri/renderD128` 完全缺失，Panthor 驱动无法初始化。 请检查`dmesg | grep -i panthor` 以了解错误。
> {.is-info}

# 4. 理解双GPU设置

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

# 启用 OpenGL 3.3 (Panfrost definition to 3.1, some applications request 3.3+)
PAN_MESA_DEBUG=gl3
```

`PAN_MESA_DEBUG=gl3`变量允许在Mali-G610 GPU上进行实验性OpenGL 3.3支持。 没有它，Panfrost只能暴露OpenGL 3.1，它会阻止像`kitty`这样的应用程序启动. 如果特定应用程序显示渲染伪影，请在没有标志的情况下启动它：

```
PAN_MESA_DEBUG=应用程序名称
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

# 🔄 3. 配置硬件视频回放的 mpv

On RK3588, `mpv` can use V4L2 Request API for hardware video decoding and Vulkan for rendering output. This bypasses the Wayland EGL path entirely, ensuring smooth playback regardless of the Muffin limitation described in the introduction.

- Install mpv and yt-dlp:

```
sudo pacman -S --needed mpv yt-dlp
```

- Create or edit the mpv configuration file:

```
nano ~/.config/mpv/mpv.conf
```

- Add the following content:

```
hwdec=v4l2request
vo=gpu-next,gpu
gpu-api=vulkan
gpu-context=waylandvk
ytdl-format=bestvideo[height<=?1080]+bestaudio
```

| Option                   | Purpose                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `hwdec=v4l2request`      | Hardware video decoding via V4L2 stateless API (zero-copy DMA-BUF) |
| `vo=gpu-next,gpu`        | Video output via libplacebo (falls back to gpu if needed)          |
| `gpu-api=vulkan`         | Use PanVK Vulkan driver (works correctly, bypasses EGL)            |
| `gpu-context=waylandvk`  | Vulkan WSI for Wayland (native, no XWayland)                       |
| `ytdl-format=...`        | Limit YouTube to 1080p to avoid overloading the hardware decoder                      |
| {.dense} |                                                                                       |

- Test playback:

```
mpv --fs https://www.youtube.com/watch?v=LXb3EKWsInQ
```

You should see `Using hardware decoding (v4l2request)` and `VO: [gpu-next]` in the output. The video should play smoothly without dropped frames.

> Without the Vulkan configuration, mpv defaults to OpenGL via the Wayland EGL path, which falls back to `llvmpipe` software rendering on Cinnamon. This causes severe frame drops (hundreds of dropped frames per minute). Always use the Vulkan configuration above.
> {.is-info}

# 9. 验证 GPU 加速

## 7.1 Check the Renderer

在Wayland，您必须使用 `eglinfo` 来检查GPU 加速。 The `glxinfo` command goes through XWayland and will show `llvmpipe` even when the compositor is GPU-accelerated (see [section 8.1](#h-81-glxinfo-still-shows-llvmpipe)).

- 安装`eglinfo` 如果不存在：

```
sudo pacman -S --needmesa-utils
```

- Check the GBM and Device renderers:

```
eglinfo -B 2>/dev/null | grep -A5 "GBM platform"
```

```
eglinfo -B 2>/dev/null | grep -A10 "Device #0"
```

You should see `Mali-G610 MC4 (Panfrost)` in both outputs, not `llvmpipe`. The renderer name `Panfrost` is correct even when using the `panthor` kernel driver — Mesa's OpenGL driver is named Panfrost for all Mali Valhall GPUs.

- Check the Wayland platform:

```
eglinfo -B 2>/dev/null | grep -A10 "Wayland platform"
```

> Due to the Muffin limitation described in the introduction, the Wayland platform may show `llvmpipe` even when the compositor is using the GPU. This is a known issue. Verify GPU acceleration using the GBM and Device platform checks above instead.
> {.is-info}

- Check Vulkan (should always work):

```
vulkaninfo --summary 2>/dev/null | grep -A3 "GPU"
```

You should see `Mali-G610 MC4` with the `panvk` driver.

## 7.2 Check Compositing Status

- 打开 Cinnamon的系统设置，导航到 `General` 并检查是否启用 `Compositing`
- 或者，从终端中检查：

```
dconf read /org/cinnamon/muffin/compositing-manager
```

输出应为“true”。

# 4. 🤝 贡献

If you encounter issues, start by generating a full system report. This collects all hardware and software information in one shot and makes it easy to get help on the [BredOS Discord](https://discord.gg/beSUnWGVH2):

```
sudo sys-report
```

This uploads the report to `termbin.com` and prints a URL you can share. To save locally instead:

```
sudo sys-report -l
```

## 8.1 glxinfo Still Shows llvmpipe

预期在韦兰会有这种情况。 `glxinfo`命令使用通过 XWayland 的 GLX 协议。 即使有完全GPU-加速的Wayland会话，`glxinfo`也可能会报告`llvmpipe`，因为XWayland可能无法访问 GPU 渲染节点。

- Use `eglinfo` instead to verify the Wayland renderer (see [section 7.1](#h-71-check-the-renderer) and [section 8.8](#h-88-wayland-egl-clients-use-llvmpipe-known-muffin-limitation))
- 要修复在 XWayland 下运行的 X11 应用程序的 "glxinfo" ，请尝试：

```
DRI_PRIME=1 glxinfo -B
```

## 8.2 Panthor Loaded but No GPU Rendering

如果`lsomd | grep panthor` 显示该模块已加载，但应用程序仍然使用 `llvmpipe`，通过这些检查：

**检查1：渲染节点存在**

```
ls -la /dev/dri/
```

- 如果 `renderD128` 丢失，Panthor 无法初始化。 检查内核日志：

```
dmesg | grep -i panthor
```

共同原因：

- 缺少固件：检查 `dmesg | grep -i 固件| grep -i mali` 。 必须安装 `mali-G610-firmware` 包，固件文件必须在 `/lib/firmware/arm/mali/arch10.8/` 中。
- 未启用设备树叠加层：如果您在内核6.1-rkr3中，请按照[设置面板](/en/how-to/how-to-setup-panthor]指南启用`rockchip-rk3588-panthor-gpu`DTBO'。

**检查 2: 用户权限**

```
ls -la /dev/dri/renderD128
组
```

如果存在`renderD128` 但您的用户不在`render` 组中，请参阅[2.3](#h-23-user-permissions)。

**勾选3： 网格检测到 GPU**

```
eglinfo -B 2>/dev/null | grep -A5 "设备平台"
```

- 如果输出显示空设备或只有`llvmpipe`, Mesa没有找到Panthor驱动器。 验证您使用的是标准的`mesa`软件包(不是 `mesa-panfork-git`)：

```
pacman -Q mesa
```

- 如果它显示 `mesa-panfork-git`, 替换它：

```
sudo pacman -S mesa
```

**勾选4： 没有冲突的 libMali**

```
pacman -Q | grep -i mali
```

- 你只能看到`mali-G610-firmware'。 如果安装了任何`libmali-valhall-g610\`软件包，它与Mesa的开源驱动程序冲突：

```
sudo pacman -R libmali-valhall-g610
```

**检查5：环境变量覆盖**

- 旧或不正确的环境变量可以强制Mesa使用错误的驱动：

```
env | grep -iE "mesa|gallium|dri|gpu|libgl|egl"
```

如果设置了任何`MESA_LOADER_DRIVER_OVERRIDE`, `LIBGL_ALWAYS_SOFTWARE`, `GALLIUM_DRIVER`, 或 `__GLX_VENDOR_LIBRARY_NAME` ，将其从您的环境配置文件中删除或将其设定。

## 8.3 Vulkan Errors (VK_ERROR_INCOMPATIBLE_DRIVER)

如果你在运行图形应用程序时看到像`ZINK: vkCreateInstance 失败 (VK_ERROR_INCOMPATIBLE_DRIVER)` 错误：

- 这意味着Mesa正在尝试使用 Zink 驱动程序(OpenGL-overVulkan)，但没有可用的 Vulkan 驱动程序。 安装 Vulkan 软件包：

```
sudo pacman -S --need vulkan-icd-loader vulkan-panfrost
```

- 验证检测到 PanVK ：

```
vulkaninfo --summary 2>/dev/null | grep -A3 "GPU"
```

你应该在输出中看到`Mali-G610`或`panvk`。

> 此错误不会阻止GPU加速OpenGL 正常工作。 如果Panthor设置正确，Mesa会使用 OpenGL 的本机Gallium 驱动程序，而不要穿过Zink/Vulkan。 然而，建议为需要Vulkan的应用程序安装 PanVK 。
> {.is-info}

## 8.4 Cinnamon Falls Back to Software Rendering

If you have confirmed that Panthor works (the checks in [section 8.2](#h-82-panthor-loaded-but-no-gpu-rendering) all pass) but Cinnamon's compositor still uses software rendering:

- 验证 udev 规则已经应用(见[4.1节] (#h-41-create-a-udev-rule):

```
udevadm info -q all -n /dev/dri/card1 | grep mutter
```

- Check that `MUTTER_ALLOW_HYBRID_GPUS=1` is set (see [section 4.2](#h-42-set-environment-variables))

- 查看 Muffin的日志错误：

```
journalctl --user -b | grep -i muffin
```

- 请确保合成未禁用：

```
dconf read /org/cinnamon/muffin/compositing-manager
```

如果输出为 'false' 或 '空白' ，则启用它：

```
dconf write /org/cinnamon/muffin/compositing-manager true
```

## 8.5 Black Screen or Login Loop

如果Wayland会话未能开始：

- 使用 `Ctrl+Alt+F2` 切换到TTY 并登录
- 检查会话日志：

```
journalctl --user -b -u cinnamon-session
```

- 作为一个工作区，从登录界面回到X11会话并验证您的配置

## 8.6 Screen Tearing or Poor Performance

如果会话开始，但性能很差：

- Verify compositing is enabled (see [section 7.2](#h-72-check-compositing-status))
- 检查系统会话是否覆盖了 Flatpak 或 Snap 版本
- 如果你看到渲染伪影，请尝试将 `CLUTTER_PAINT=disable-culling` 添加到 `/etc/environment.d/90-rk3588-gpu.conf`

## 8.7 Reverting to X11

如果Wayland工作不正确， 您总是可以通过选择 `Cinnamon` 会话切换回X11 (没有"航行"标签)。

## 8.8 Wayland EGL Clients Use llvmpipe (Known Muffin Limitation)

If the GBM and Device platforms in `eglinfo` correctly show `Mali-G610 MC4 (Panfrost)` but the Wayland platform shows `llvmpipe`, this is a known limitation in Muffin `6.6.x`.

**Explanation:** Muffin uses the GPU correctly for its own desktop compositing (via GBM). However, it advertises the wrong DRM device to Wayland clients via the `wl_drm` protocol. It announces `card0` (rockchip-drm, display controller with no 3D capabilities) instead of `card1`/`renderD128` (panthor, the GPU). All Wayland EGL clients inherit this wrong device and fall back to `llvmpipe`.

GNOME's Mutter solves this with the [`meta_is_udev_device_preferred_primary()`](https://gitlab.gnome.org/GNOME/mutter/-/blob/main/src/backends/meta-udev.c) function, which reads the `mutter-device-preferred-primary` udev tag. Muffin has not yet ported this function from upstream Mutter. The udev rule from [section 4.1](#h-41-create-a-udev-rule) is still recommended (other compositors and future Muffin versions will use it), but it has no effect on current Muffin versions.

- Verify the limitation by checking what DRM devices Muffin has open:

```
ls -la /proc/$(pgrep -f 'cinnamon --replace' -o)/fd 2>/dev/null | grep dri
```

You should see both `card0` and `renderD128` open, confirming Muffin is using the GPU for compositing.

**What works despite this limitation:**

| Component                                              | Status                                 | Reason                      |
| ------------------------------------------------------ | -------------------------------------- | --------------------------- |
| Desktop compositing                                    | GPU-accelerated                        | Muffin uses GBM directly    |
| Vulkan apps (mpv, vkmark, browsers) | GPU-accelerated                        | PanVK bypasses EGL entirely |
| Wayland EGL apps (GTK OpenGL)       | Software (llvmpipe) | Wrong DRM device advertised |
| {.dense}                               |                                        |                             |

**Workarounds:**

- Use Vulkan rendering where possible (see [section 6](#h-6-configure-mpv-for-hardware-video-playback) for mpv)
- Use GNOME or KDE Wayland instead, which handle multi-GPU correctly on the same hardware
- Track the upstream issue: [linuxmint/muffin](https://github.com/linuxmint/muffin/issues)

# 10. Summary

- 下表汇总了所需的变化：

| 什么                       | 文件                                          | 内容                                                    |
| ------------------------ | ------------------------------------------- | ----------------------------------------------------- |
| Udev 规则                  | `/etc/udev/rules.d/61-mutter-Panthor.rules` | 标记`card1`为`突变设备-首选原始`                                 |
| 环境                       | `/etc/environment.d/90-rk3588-gpu.conf`     | `MUTTER_ALLOW_HYBRID_GPUS=1` and `PAN_MESA_DEBUG=gl3` |
| mpv config               | `~/.config/mpv/mpv.conf`                    | Vulkan rendering + V4L2 hardware decoding             |
| 会议                       | 登录屏幕                                        | 选择 `Cinnamon (Wayland)`                               |
| {.dense} |                                             |                                                       |

# 10. 参考

- [Muffin 源代码](https://github.com/linuxmint/muffin) - Linux Mint
- [完全多GPU支持](https://gitlab.gnome.org/GNOME/mutter) - GNOME
- [Mutter `meta_is_udev_device_preferred_primary` implementation](https://gitlab.gnome.org/GNOME/mutter/-/blob/main/src/backends/meta-udev.c) - GNOME (missing in Muffin)
- [Mesa Panfrost driver documentation](https://docs.mesa3d.org/drivers/panfrost.html) - Mesa
- [设置马里的Panthor 与 RK3588](https://wiki.bredos.org/en/how-to/how-to-setup-panthor) - BredOS Wiki
- [BredOS sys-report](https://github.com/BredOS/sys-report) - System diagnostics tool
- [kitty OpenGL 3.3 workaround](https://github.com/kovidgoyal/kitty/issues/2790#issuecomment-969195133) - PAN_MESA_DEBUG=gl3
- [Armbian RK3588 GPU 加速讨论](https://forum.armbian.com/topic/56374-expected-default-graphics-acceleration-for-rk3588/) - Armbian Forum