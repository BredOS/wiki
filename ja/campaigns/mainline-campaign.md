---
title: メインライン キャンペーン
description:
published: true
date: 2025-09-23T18:06:18.145Z
tags:
editor: markdown
dateCreated: 2025-09-22T17:56:04.573Z
---

# このキャンペーンに資金を追加する

## Mainline RK3588 Support in BredOS

今のところ、RK3588デバイス用のブレッドOS画像は、巨大なロックチップBSPカーネルに依存しています。 維持が困難で、安全ではない、そして常に上流Linuxより大きく遅れているダクトテープ付きのコードベース。

私たちはそれを変えたいのです

RK3588をサポートすることで、ブレッドOSは以下のようになります。

- 長期的なメンテナンス性(これ以上BSPハックを追跡しない)

- Latest upstream kernel security fixes

- パフォーマンスと安定性の向上

- すべてのRK3588デバイス(SBC、開発ボード、ミニPC)をサポート

- ARM64デスクトップとサーバー使用のための強固な基礎

これは、BredOS とより広範な Linux エコシステムを、RK3588 ハードウェアを使用するすべての人にとってより良いものにすることについてです。

> Our goal with this campaign is to raise atleast **2500€**, so that we can port approximately 28 boards.
> {.is-warning}

## なぜ私たちはこれを行っているのですか?

私たちがよく耳にする公正な質問は次のとおりです。_「RK3588はすでに主流になっていませんか？」_\
真実は、**その一部だけ**です。

低レベルのバックエンドの仕事 (基本的なカーネルサポートのような) の多くが上流に上陸していますが、**日々の必需品はまだ壊れているか行方不明**。

- Many Wi-Fi/Bluetooth drivers don’t work out of the box
- デバイス固有の最適化は、一般的なメインラインパッチではカバーされません

BredOS では、RK3588 デバイスを \*\*実際のユーザー向けに実用的で洗練されたものにしたいと考えています。 それは次のことを意味します: それは次のことを意味します:

- 信頼性の高いWi-Fiとネットワーク
- Tuned fan profiles (quiet when idle, cooling under load)
- 安定した GPU とマルチメディアのサポート
- Proper installer and images
- Frequently updated images

このキャンペーンは「起動」についてだけではありません。
It’s about making RK3588 devices **actually usable** as fully featured desktop computers.

## メインラインの利点

初期のメインライン実験のおかげで、すでにいくつかのエキサイティングな利点があります。

- **2×Vulkanパフォーマンス** BSPビルドとGPUグッズより
- **適切なVPU実装** カスタムRockchip メディア処理プラットフォーム (MPP) を必要としません
- **Chromiumまたは任意のビデオアクセラレーションアプリ**をすぐに実行する機能
- 一般的なビデオワークロードのカスタムハックや再コンパイルはありません

メインラインは、開発者とエンドユーザーの両方に対して、これらの**本物の目に見える改善**を解放し、RK3588デバイスは日常的に使用することができます。

## 支援方法

- **寄付**: 寄付するたびに、メインのRK3588体験に近づきます。 [here](https://ko-fi.com/Z8Z3I4J0P) または PM @rippanda12 を寄付できます [here](https://ko-fi.com/Z8Z3I4J0P) または PM @rippanda12 を寄付できます
- **Share**: RK3588コミュニティ、SBCフォーラム、ソーシャルメディアに広めましょう。
- **スポンサー**: RK3588ハードウェアに依存する企業は、より高い階層でこのマイルストーンを取り戻すことができます(私たちは私たちのリポジトリとウェブサイトでスポンサーをクレジットします)。
- **Testing and reporting**: We need a lot of testing, especially on weird apps and desktop workloads.

## 私たちが目指すこと

1. **アップストリーミングとカーネルワーク**
   - メインラインカーネルにパッチをリベース

2. **Boot & Install Support**
   - 標準ARM64ブートフロー(可能な限りUEFI) のサポート
   - RK3588ボードに適切なBredOSメインライン画像を作成する

3. **Testing & CI**
   - 人気のボード用の自動テストビルド(Orange Pi 5, Rock 5Bなど)
   - メインラインの更新との継続的な統合

4. **ユーザーエクスペリエンス**
   - GPU、ネットワーク、ストレージ、およびI/Oが安定していることを確認してください
   - エンドユーザーに事前構築済みのフラッシュ画像を提供する

5. **Security**
   - Keeping track of upstream security fixes, providing a stable secure kernel
   - Encrypted password protected root filesystem during setup
   - Password protected GRUB

## お金がどこに行くか

- 開発者時間 (カーネル、ブートローダー、ユーザースペースの統合)
- 継続的なビルドとテストのためのCIインフラストラクチャ

The bigger the budget at our disposal, the more time we can dedicate to BredOS.

### **[Support the RK3588 Mainline Milestone Now](https://ko-fi.com/Z8Z3I4J0P)**

---