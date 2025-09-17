---
title: Radxa Orion O6
description:
published: false
date: 2025-09-17T06:13:49.328Z
tags:
editor: markdown
dateCreated: 2025-09-17T06:04:34.142Z
---

# 1. はじめに

Radxa Orion O6は、Cix P1(CD8180)SoCを搭載したMini-ITXマザーボードで、12コアARMv9を搭載しています。 4つの大きなCortex‐A720コア(約2.8GHz)、4つの中型A720s(約2.4GHz)、4つの小さなCortex‐A520s(約1.8GHz)を持つCPU。  Arm Immortalis‐G720 GPUと、AI推論用の30 TOPS NPUが含まれています。  最大64 GB LPDDR5、複数のディスプレイ出力、デュアル 5 GbE ネットワーキング、および PCIe Gen 4 拡張を備えています。 エッジAI、マルチメディア、および開発ワークステーションアプリケーションを目的としています。

> パンダのタイピングスキルのおかげで、「_プリオン_」とあだ名されました。
> {.is-info}

# 2. ダウンロード

私たちの[Github page](https://github.com/BredOS/bredos-iso/releases/latest)でaarch64 isoのダウンロードリンクを見つけることができます!

# 3. インストール

プリオンは、デバイス固有の画像を使用する他のサポートされているシングルボードコンピュータ(SBC)とは異なり、一般的なISOイメージからのインストールをサポートしています。 インストールは、USBスティックまたはUSB光学ドライブを使用して行うことができます。

## 3.1 Generic ISO のインストール

インストール用のガイドはこちらからご覧いただけます。

## 3.2 UEFI インストール

私たちはRadxaのソースコードに基づいたカスタムUEFIを開発しました。 ボードが販売されている実際のCPU速度に対応しています。 PCIeのリンク速度を制御することができます。そして、すべての最高のものは、起動時にBredロゴを表示します。 UEFIを更新するためのガイドはこちらからご覧いただけます。