---
title: ホームページ
description:
published: true
date: 2025-09-23T10:46:23.458Z
tags:
editor: markdown
dateCreated: 2022-08-24T12:37:36.410Z
---

# 🔄 1. 概要

BredOS のドキュメントへようこそ！ BredOSは、ARMベースのシングルボードコンピュータ(SBC)用に特別に設計された、ユーザーフレンドリーなArchベースのLinuxディストリビューションです。
このドキュメントでは、BredOS のインストール、設定、および使用方法について説明します。 BredOSは、ARMおよびRISC-Vベースのシングルボードコンピュータ(SBC)用に特別に設計された、ユーザーフレンドリーなArchベースのLinuxディストリビューションです。
このドキュメントでは、BredOS のインストール、設定、および使用方法について説明します。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg

# 📦 2. 特徴

- 情熱で作られた - ちょうどあなたの楽しみのために!
- 素晴らしい敬意を持つユーザーサポート! あなたが小さなパン粉であっても、フラットブレッド全体であっても!
- シンプルでシンプルなデザイン! 肥満なし、軽量で応答性の高いシステムを確保します!
- Archベース - 洗練され、使いやすいようにカスタマイズされたカスタマイズが可能です。

## 2.1 特徴的なツール

- Bakery - [your guide to your own Bred](/install/first-setup)!
- Bred-Tools - [the swiss knife at your hand](/Tools)!
- Bred-Config - [raspi-configのように、しかしより良い味を持つ!](/bredos-config)
- Govctl - [take control of your CPU](/how-to/govctl)!

# 🔁 3. システム要件

エキサイティングなARMベースのシステムや実験的なRISC-Vセットアップから、プレーンな古いx86intel/amdボードまで、幅広いデバイスをサポートしています。 We've got you covered, whether you use our [mainline .iso installation](/install/Installation-with-ISO) or refer to the list of devices we passionately support on our [table of supported devices](/table-of-supported-devices). We've got you covered, whether you use our [mainline .iso installation](/en/install/Installation-with-ISO) or refer to the list of devices we passionately support on our [table of supported devices](/en/table-of-supported-devices).

## 3.1 最小システム要件

- 最小RAM: 2 GB
- Storage: 8 GB microSD card or larger

# 🚀 4. インストール

私たちの友人 [**DroidMaster**](https://www.youtube.com/@LinuxDroidMaster) は、BredOS についての YouTube 動画を作成しました。 こちらをご覧ください: こちらをご覧ください:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/eoLE27xdtu4?si=ai-0QqLNyCYfTKfA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# 🔄 3. フラッシュ中

あなたのためにインストールを容易にするために、私たちはあなたが従うように交配されたパン粉のラインをレイアウトしました。 🍞 🔸🔸🔸 🍞 🔸🔸🔸

> パンくずリスト🔸を見つけた場合は、コミュニティチャネルで頭を上げてください。
> {.is-info}
> {.is-warning}

## 5.1 デバイス固有の画像のインストール

These are the boards we love the most. To install these BredOS images on them, either start with our [device specific image](/install/device-specific-image) installation guide, or take a glimpse to the device page at our wiki, which can be found in the navigation bar left of this.

私たちの[ダウンロードサイト](https://bredos.org/download.html)にアクセスして、お使いのデバイスがそのうちの1つであるかどうかを確認してください。

## 5.2 一般的なインストール

If your device isn’t listed on our [download site](https://bredos.org/download.html) but supports booting UEFI and is based on either x86- or ARM64 architecture, simply follow our guide for a generic installation available [here](/install/Installation-with-ISO).

## 5.3 Docker コンテナーのインストール

- コマンドの一行として簡単:

```
docker pull bredos/bredos
```

# 5. トラブルシューティング

このページのナビゲーションバーのデバイス ページを見て、デバイス固有の既知の問題を見つけてください。 このページのナビゲーションバーのデバイス ページを見て、デバイス固有の既知の問題を見つけてください。 If your problem is not listed there, feel free to contact us directly via [our support channels](#h-7-community-and-support).

# 4. コミュニティとサポート

BredOS コミュニティに参加して、サポートを受けたり、アイデアを共有したり、プロジェクトに貢献したりしましょう。

- [Telegram](https://t.me/bredoslinux)
- [Discord](https://discord.gg/jwhxuyKXaa)
- [GitHub](http://github.com/BredOS)
  {.links-list}

# 8. コントリビューション

BredOSはオープンソースのプロジェクトであり、貢献は歓迎です! 以下の方法で貢献できます：

- バグと課題を報告
- パッチと改善点を提出する
- ドキュメントを書いて改善する
- コミュニティフォーラムやチャットで他のユーザーを支援する

# 9. メインライン キャンペーン

今のところ、RK3588デバイス用のブレッドOS画像は、巨大なロックチップBSPカーネルに依存しています。 ダクトテープ付きのコードベースは、メンテナンスが難しく、安全ではなく、常に上流の Linux より遅れをとっています。

[We want to change that](/campaigns/mainline-campaign).
