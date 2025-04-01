---
title: Switch Desktop Environments to Use GNOME on BredOS
description: Learn how to install and switch to the GNOME desktop environment on BredOS
published: true
date: 2025-02-23T15:13:50.035Z
tags: customization
editor: markdown
dateCreated: 2025-02-23T15:13:50.035Z
---

# 🎨 GNOME Desktop on BredOS

The GNOME desktop environment can be installed with the AUR package `gnome-meta`.\
To install it, run:

```
yay -S gnome-meta
```

---

## 🔄 Switch to GDM

For proper operation, you need to switch to **GDM** after installation.\
Run the following commands:

```
sudo systemctl disable lightdm
sudo systemctl enable gdm
```

📝 **Note:** Only GNOME on Wayland is supported.

---

## 🔄 🖥️ Screen Rotation Fix

**If** your screen rotates incorrectly, you can install and configure the **Screen Rotate** extension.

### 1️⃣ Install Extension Manager

Run:

```
sudo pacman -S extension-manager
```

Once installed, open the application.

### 2️⃣ Install Screen Rotate

Inside the application:

- Tap `Browse` > `Search`
- Type **Screen Rotate**
- Install `Screen Rotate` by **shyzus**.

### 3️⃣ Configure Screen Rotate

- Go to the `Installed` tab in Extension Manager.
- Tap the ⚙️ icon to open the extension settings.
- Increase the **Set orientation offset** value to `1`.

---

✅ Done! GNOME is now properly set up on BredOS. 🚀
