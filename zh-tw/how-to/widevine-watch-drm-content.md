---
title: 🎥 How to play back DRM protected content (installing widevine)
description: Learn how to enable playback of DRM-protected content on BredOS by installing the Widevine plugin
published: true
date: 2024-09-20T14:44:32.766Z
tags: null
editor: markdown
dateCreated: 2024-08-28T05:58:27.563Z
---

# 🎥 How to play back DRM protected content (installing widevine)

Learn how to enable playback of DRM-protected content on BredOS by installing the Widevine plugin.

## 🛠️ Steps to Install Widevine

1. **🔧 Install Widevine**\
   Open your terminal and run the following command to install Widevine for aarch64 architecture:

```
sudo pacman -S widevine-aarch64
```

2. **🔄 Reboot Your System**\
   After installation, reboot your system to ensure the changes take effect.

3. **🍿 Setting Up for Netflix**
   To watch Netflix, you'll need to spoof your user agent. Use the following user agent string:

```
Mozilla/5.0 (X11; CrOS aarch64 15236.80.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.125 Safari/537.36
```

You can easily spoof your user agent by installing this Firefox extension: [User-Agent String Switcher](https://addons.mozilla.org/en-GB/firefox/addon/user-agent-string-switcher/)
