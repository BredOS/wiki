---
title: 浏览器设置
description: 在 ARM64 板上使用 BredOS 设置一个GPU加速浏览器
published: true
date: 2026-03-07T16：35：11.784Z
tags: 浏览器、 铬、 gpu、 wayland、 arm64
editor: markdown
dateCreated: 2026-03-07T16：08：59.754Z
---

# 2. 介绍信息

运行BredOS 的ARM64 板通过 Panfrost (OpenGL ES3.1) 和 PanVK (Vulkan 1.4) Mesa 驱动程序具有完全的 GPU 加速功能。 然而，并非所有浏览器都能平等地利用这种机会。 本指南包括通过 Flatpak设置 `Ungoogled Chromium` ，最优化的 GPU 旗帜，用于平稳浏览体验。

> 目前没有任何浏览器通过 V4L2 无条件的 API 支持硬件视频解码。 关于硬件加速的视频播放，见部分 [5。 YouTube硬件解码](#h-5-youtube-with-hardware-decode)。
> {.is-info}

# 3. 浏览器比较

- 下表比较了ARM64上的主要浏览器选项和 BredOS：

| 功能                       |           未oged Chromium (Flatpak)           |               Firefox / LibreWolf              |
| ------------------------ | :-------------------------------------------------------------: | :--------------------------------------------: |
| GPU 组成                   | 全(ANGLE + Panfrost GLES 3.1) | partial(WebRender, 较少优化ARM) |
| GPU 光栅化                  |                               所有页面                              |                       限量的                      |
| WebGL                    |                              硬件加速了                              |                      硬件加速了                     |
| WebGPU                   |                              硬件加速了                              |                       不支持                      |
| 零拷贝组成                    |                               支持的                               |                       不支持                      |
| 视频解码                     |                               仅软件                               |                       仅软件                      |
| Wayland                  |                    本机(臭氧)                    |                       原生的                      |
| 平板可用性                    |                                可用                               |                       可用                       |
| {.dense} |                                                                 |                                                |

Chromium的非通用后端映射到Panfrost的 OpenGL ES3.1，提供了完整的硬件加速页面渲染、合成和WebGL/WebGPU。 适用于 ARM Mali GPU 的 Firefox WebRender 的优化程度较低。

> **Flatpak中的 GPU 堆栈**：Flatpak 运行时间包括Panthor DRI + PanVK (Vulkan 1.4) + Panfrost (GLES 3.1). 使用 `devices=all` 和 `sockets=wayland` 权限，沙盒可以完全访问 GPU 。
> {.is-info}

# 4. 安装 rkdeveloptool

## 3.1 Install Flatpak

- 安装 Flatpak 并添加 Flathub 仓库：

```
sudo pacman -S flatpak
sudo flatpak remote-added --if-not-exists flathuthub https://dl.flathub.org/repo/flathub.flatpakrepo
sudo flatpak 更新 --appstream
```

## 3.2 安装 Ungoogled Chromium

- 从Flathub安装浏览器：

```
sudo flatpak install -y flathub io.github.ungoogled_software.ungoogled_chromium
```

# 5. GPU 加速设置

## 4.1 带GPU标志的桌面输入

若要在Wayland上以完全GPU加速度启动 Chromium ，请创建自定义桌面条目。

- 创建桌面项：

```
mkdir -p ~/.local/share/applications
cat > ~/.local/share/applications/ungoogled-chromium-gpu。 esktop <'EOF'
[桌面条目]
Type=Application
名称=Ungoogled Chromium (GPU)
Comment=Web Browser 与 Wayland + Vulkan GPU 加速
Exec=flatpak 运行 io.github.ungoogled_software。 ngoogled_chromium --ignore-gpu-blocklist --enable-Nuclear copy --ozo platform=wayland --use-gl=egl --enable-features=Vulkan,Vulkan,Vulkan,FromANGE,DefaultANGLEVulkan,WaylandWindowDecorations
Icon=io.github.ungoogled_software.ungoogled_chromium
Categories=Network;WebBrowser;
Startupnotefy=true
EOF
update-desktop data ~/.local/share/applications/
```

## 4.2 旗帜参考

- 每个国旗都有一个特定的目的：

| 标志                                          | 目的                                     |
| ------------------------------------------- | -------------------------------------- |
| `--ozone-platform=wayland`                  | 本土的瓦地-避免XWayland的间接费用                  |
| `--use-gl=egl`                              | 直接使用EGL (Wayland需要) |
| `--ignore-gpu-blocklist`                    | 允许ARM GPU加速度                           |
| `--enable-零拷贝`                              | GPU 和合成器之间零复制缓冲区共享                     |
| `Vulkan,VulkanFromANGLE,DefaultANGLEVulkan` | 透过PanVK Vulkan 1.4渲染   |
| `WaylandWindowDecorations`                  | Wayland下的本机窗口装饰                        |
| {.dense}                    |                                        |

> **备份**：如果Vulkan在你的板上造成崩溃，则从`--enable-features`中移除3个Vulkan特征，并且只保留`--use-gl=egl`。 这可以通过Panfrost返回OpenGL ES, 而后者仍然是硬件加速。
> {.is-info}

## 4.3 验证 GPU 加速

使用 GPU 标志启动 Chromium 后：

- 在地址栏中打开 `chrome://gpu` 。

您应该看到：

- **GL_RENDER**: `Mali-G610` / `panfrost` / `panvk` (不是 `SwiftShader` 或 `lvmpipe`)
- **Canvas**: 硬件加速了
- **组合**：硬件加速了
- **Rasterization**：硬件加速了
- **WebGL**：硬件加速
- **WebGPU**：硬件加速

> 如果`GL_RENDER`显示`SwiftShader`或`llvmpipe`，GPU加速则未激活。 Check that Flatpak has `devices=all` permission: `flatpak info --show-permissions io.github.ungoogled_software.ungoogled_chromium`
> {.is-warning}

# 4. Youtube 硬件解码器

ARM64 上没有浏览器支持 V4L2 无国籍解码，这是在主线RK3588 内核上使用的硬件视频解码方法。 若要以硬件加速播放YouTube视频，请使用 `mpv` + `yt-dlp`。

## 5.1 安装mpv 和 yt-dlp

- 安装必需的软件包：

```
sudo pacman -S mpv yt-dlp
```

## 5.2 从终端播放

- 用硬件解码播放YouTube视频：

```
mpv 'https://youtube.com/watch?v=VIDEO_ID'
```

`mpv` 自动使用 `yt-dlp` 方法解压视频 URL 和 RKVDEC2 来解码硬件。

## 5.3 从浏览器播放(书签)

您可以直接从 Chromium 创建一个书签来打开当前页面。

- Create a protocol handler script:

```
mkdir -p ~/.local/bin
cat > ~/.local/bin/mpv-handler.sh << 'SCRIPT'
#!/bin/sh
url=$(echo "$1" | sed 's|^mpv://||')
exec mpv "$url"
SCRIPT
chmod +x ~/.local/bin/mpv-handler.sh
```

- 为 'mpv://' 协议创建桌面条目：

```
cat > ~/.local/share/applications/mpv-handler.desktop << 'EOF'
[Desktop Entry]
Type=Application
Name=mpv URL Handler
Exec=/home/$USER/.local/bin/mpv-handler.sh %u
MimeType=x-scheme-handler/mpv;
NoDisplay=true
EOF
xdg-mime default mpv-handler.desktop x-scheme-handler/mpv
```

- 将此书签添加到您的浏览器书签栏：

```
javascript:void(window.open('mpv://'+location.href))
```

点击任意YouTube页面上的书签，用硬件加速解码来打开它。

# 🔄 3. 🤝 贡献

## 6.1 Chromium 显示软件渲染器

如果`chrome://gpu`显示软件渲染：

- 验证 Flatpak GPU 权限：

```
flatpak info --show-permissionio.github.ungoogled_software.ungoogled_chromium
```

输出应该包含 `devices=all` 和 `sockets=wayland` 。 如果不是:

- 手动覆盖权限：

```
flatpak override --user --device=all io.github.ungoogled_software.ungoogled_chromium
flatpak override --user --socket=wayland io.github.ungoogled_software.ungoogled_chromium
```

## 6.2 Chromium 撞击了Vulkan 旗帜。

有些板块或网格版本可能与 PanVK 有问题。 删除Vulkan功能。

- 使用这个更简单的旗帜设定：

```
flatpak 运行 io.github.ungoogled_software.ungoogled_chromium --ignore-gpu-blocklist --enable-Non-copy --ozone platform=wayland --use-gl=egl --enable-features=WaylandWindowDecorations
```

这仍然是通过 Panfrost (OpenGL ES) 使用 GPU 加速，而无需使用 Vulkan 路径。

## 6.3mpv 不使用硬件解码

- 验证 RKVDEC2 可用：

```
ls /dev/video-dec0
```

如果设备节点丢失，请检查内核模块是否已加载：

- 检查 RKVDEC2 模块：

```
lsmod | grep rockchip_vdec
```

# 9. 参考

- [Chromium GPU Acceleration docs](https://chromium.googlesource.com/chromium/src/+/main/docs/gpu/gpu_testing.md) - Chromium Project
- [Mesa Panfrost 驱动器](https://docs.mesa3d.org/drivers/panfrost.html) - Mesa
- [Mesa PanVK driver](https://docs.mesa3d.org/drivers/panvk.html) - Mesa
- [Flatpak 文档](https://docs.flatpak.org/) - Flatpak
- [mpv manual](https://mpv.io/manual/stable/) - mpv