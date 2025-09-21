---
title: BredOS の設定
description:
published: false
date: 2025-09-21T09:27:32.905Z
tags:
editor: markdown
dateCreated: 2025-09-21T09:27:04.136Z
---

# 1. はじめに

- 「bredos-config」ツールは、システムの変更、メンテナンス、管理を簡素化するために開発されました。

![main.png](/bredos-config/main.png)

> `bredos-config`ツールはデフォルトでインストールされています。
> {.is-info}

- 削除した場合および/または再インストールしたい場合は、以下を実行してください:

```
sudo pacman -S bredos-config
```

# 2. 特徴

## 2.1 デバイス ツリー マネージャー

- このオプションは、カーネルとデバイスの相互作用を変更するために使用されるデバイス ツリーとデバイス ツリー オーバーレイを管理するのに役立ちます。 簡単な例は、Orange Pi 5 PlusのLEDを無効にするためにそれらを使用することですが、さらに詳しく調べることができます。 Follow [this article](/how-to/how-to-enable-dtbos) to learn more about it.

![dtb-manager.png](/bredos-config/dtb-manager.png)

## 2.2 システムを更新

> このオプションは現在構築中です！
> {.is-warning}

## 2.3 システムの維持

- この項では、 ファイルシステムメンテナンスのタスクを実行したり、システムの完全性を確認したりするように、システムをきれいに保ちスムーズに実行するための便利なタスクがいくつかあります。

![upkeep.png](/bredos-config/upkeep.png)

## 2.4 システムの調整

- ここでは、システムにいくつかの便利な調整を見つけることができます:

![tweaks.png](/bredos-config/tweaks.png)

## 2.5 移行

> なぜシステム調整に統合されなかったのですか?
> {.is-danger}

## 2.6 パッケージ

- ここでは、蒸気やドッカーなどのクールなものを正しくインストールするためのさまざまなフックを見つけることができます。

![packages.png](/bredos-config/packages.png)