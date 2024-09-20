---
title: 🎥 如何回放 DRM 保护的内容 (安装广泛)
description: 通过安装 Widevine 插件学习如何在 BredOS 上启用 DRM保护内容的回放
published: true
date: 2024-09-20T14:44:32.766Z
tags: null
editor: markdown
dateCreated: 2024-08-28T05:58:27.563Z
---

# 🎥 如何回放 DRM 保护的内容 (安装广泛)

通过安装 Widevine 插件学习如何在 BredOS 上启用 DRM保护内容的回放。

## 🛠️ 安装宽体的步骤

1. **🔧 安装 Widevine**\
   打开您的终端并运行以下命令来安装 Widevine：

```
sudo pacman -S widevine-aarch64
```

2. **:countrockwise_arrows_buton：重新启动系统**\
   安装后，重启系统以确保更改生效。

3. **🍿 设置 Netflix**
   要观看Netflix，您需要弄清楚您的用户代理人。 使用以下用户代理字符串： 使用以下用户代理字符串：

```
Mozilla/5.0 (X11; CrOS aarch64 15236.80.0.0) AppleWebKit/537.36 (KHTML, such Gecko) Chrome/109.0.5414.125 Safari/537.36
```

您可以通过安装此 Firefox 扩展轻松地篡改您的用户代理： [User-Agent String Switcher](https://addons.mozilla.org/en-GB/firefox/addon/user-agent-string-switcher/)
