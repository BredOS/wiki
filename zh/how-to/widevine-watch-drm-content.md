---
title: 如何播放 DRM 受保护的内容(安装宽带)
description: 通过安装 Widevine 插件学习如何在 BredOS 上启用 DRM保护内容的回放
published: true
date: 2025-09-15T09：17：04.241Z
tags:
editor: markdown
dateCreated: 2024-08-28T05:58:27.563Z
---

# 1. 简介

通过安装 Widevine 插件学习如何在 BredOS 上启用 DRM保护内容的回放。

# 2. 宽度：

## 2.1 安装 Widevine

- 打开您的终端并运行以下命令来安装 Widevine：

```
sudo pacman -S widevine-aarch64
```

## 2.2 重启系统

- 安装后，重启系统以确保更改生效。

## 2.3 为Netflix 设置

- 要观看Netflix，您需要弄乱您的用户代理。 使用以下用户代理字符串：

```
Mozilla/5.0 (X11; CrOS aarch64 15236.80.0.0) AppleWebKit/537.36 (KHTML, such Gecko) Chrome/109.0.5414.125 Safari/537.36
```

> 您可以轻松地通过安装此 Firefox 扩展来破坏您的用户代理: [User-Agent String Switcher](https://addons.mozilla.org/en-GB/firefox/addon/user-agent-string-switcher/)
> {.is-info}


