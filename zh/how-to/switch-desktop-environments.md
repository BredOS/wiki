---
title: 切换桌面环境以在 BredOS 上使用 GNOME
description: 学习如何在 BredOS 上安装并切换到 GNOME 桌面环境
published: true
date: 2025-02-23T15:13:50.035Z
tags: 自定义设置
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 🎨 BredOS 上的 GNOME 桌面

GNOME 桌面环境可以安装在 AUR 包 `gnome-meta` 中。\
要安装它，请运行：

```
yay -S gnome-meta
```

---

## 🔄 切换到 GDM

要正常操作，您需要在安装后切换到 **GDM**。\
运行以下命令：

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

📝**注意:** 仅支持 Wayland 上的 GNOME。

---

## 🔄🖥️ 屏幕旋转修复

**如果** 您的屏幕旋转不正确，您可以安装和配置**屏幕旋转** 扩展。

### 1️⃣ 安装扩展管理器

运行：

```
sudo pacman -S extension-manager
```

安装完毕后，打开应用程序。

### 2️⃣ 安装屏幕旋转

应用程序内：

- 点击 `Browse` > `Search`
- 输入 **屏幕旋转**
- 通过 **shyzus** 安装 `Screen Rotate`。

### 3️⃣ 配置屏幕旋转

- 转到扩展管理中的`已安装`选项卡。
- 点击 ⚙️ 图标打开扩展设置。
- 将 **设置方向偏移** 值增加到 `1`。

---

✅ 完成！GNOME 现在已经在 BredOS 上正确设置。🚀
