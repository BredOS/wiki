---
title: 如何在 ARM 上安裝 Steam
description: null
published: true
date: 2024-07-20T08:56:15.971Z
tags: null
editor: markdown
dateCreated: 2024-07-20T07:04:41.476Z
---

# 在 BredOS (ARM) 上安裝 Steam

這份指南將引導你完成在 BredOS 上安裝 Steam 的過程，包括添加 BredOS 多庫存儲庫以及安裝 `box86-rk3xxx` 和 `box64-rk3xxx` 以實現 ARM 的相容性。

## 目錄

1. [更新系統](#步驟-1更新系統)
2. [添加 BredOS 多庫存儲庫](#步驟-2添加-bredos-多庫存儲庫)
3. [更新 Pacman 資料庫](#步驟-3更新-pacman-資料庫)
4. [安裝 Box86 和 Box64](#步驟-4安裝-box86-和-box64)
5. [安裝 Steam](#步驟-5安裝-steam)
6. [執行 Steam](#步驟-6執行-steam)

## 步驟 1：更新系統

在開始之前，請確保你的系統是最新的。

```bash
sudo pacman -Syu
```

## 步驟 2：添加 BredOS 多庫存儲庫

要安裝 Steam 和必要的翻譯層，你需要添加 BredOS 多庫存儲庫。用 root 權限的文字編輯器打開你的 `/etc/pacman.conf` 檔案。

```sh
sudo nano /etc/pacman.conf
```

然後將以下行添加到文件末尾：

```ini
[BredOS-multilib]
Include = /etc/pacman.d/bredos-mirrorlist
```

保存檔案並退出文字編輯器（<kbd>Ctrl</kbd> + <kbd>X</kbd>，然後 <kbd>Ctrl</kbd> + <kbd>Y</kbd>，然後 <kbd>Enter</kbd>）。

## 步驟 3：更新 Pacman 資料庫

添加多庫存儲庫後，更新 pacman 資料庫以包含新存儲庫。

```bash
sudo pacman -Syy
```

## 步驟 4：安裝 Box86 和 Box64

由於 Steam 和許多其遊戲是為 x86 架構構建的，你需要安裝 box86-rk3xxx 和 box64-rk3xxx 以便在你的 ARM 裝置上運行它們。

```bash
sudo pacman -S box86-rk3xxx box64-rk3xxx
```

## 步驟 5：安裝 Steam

現在，你可以從多庫存儲庫安裝 Steam。

```bash
sudo pacman -S steam
```

## 步驟 6：執行 Steam

一切安裝完成後，你現在可以執行 Steam。只需從應用啟動器中打開 steam 或在終端中輸入以下命令：

```bash
steam
```
