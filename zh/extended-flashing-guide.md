---
title: 扩展刷新指南
description: 如何使用 RKDevelop 工具
published: true
date: 2025-09-28T13:04:20.111Z
tags:
editor: markdown
dateCreated: 2025-09-28T13:02:13.948Z
---

好吧，你只是想要更多进度条在你的生活中，对吗？
We gotya covered :thumbsup: don't worry.

## 正在读取选定的闪光介质信息

- `sudo rkdeveloptools rfi`

此命令将向您显示所选闪光介质的详细信息。
默认情况下，这通常是 eMMC，除非它不可用。

```
[bill88t@prion | ~/Downloads]> sudo rkdeveloptool rfi
Flash Info:
	Manufacturer: SAMSUNG, value=00
	Flash Size: 14910 MB
	Flash Size: 30535680 Sectors
	Block Size: 512 KB
	页面大小: 2 KB
	ECC Bits: 0
	访问时间: 40
	Flash CS: Flash<0>
```

## 更改闪光目标

想要刷入/转储不是eMC，而是一个不同的东西？

- `sudo rkdeveloped tools cs 2` 用于选择SD卡。
- `sudo rkdeveloped tools cs 9` 用于选择SPINOR芯片。
- `sudo rkdeveloped tools cs 1`再次选择 eMMC 。

更改将反映在`sudo rkdeveloptool rfi`中。