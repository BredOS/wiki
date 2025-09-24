---
title: RK3588のデフォルトブートオーダーを変更する方法
description: UEFIファームウェア設定を使用して、RK3588ベースのデバイスでデフォルトの起動順序を変更する方法を学びます。
published: true
date: 2025-09-15T11:15:39.364Z
tags:
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 1. はじめに

BredOS を実行している RK3588 ベースのデバイスでブート順序を変更する必要がある場合は、次の手順に従います。

# 2. UEFIへのアクセス

## 2.1 ブートメニューへのアクセス

- デバイスをオンにして、起動中にBredOS のロゴが表示されるのを待ちます。
- ロゴが表示されている間、`ESC`キーを一度押してUEFIメニューに入ります。

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

## 2.2 ブート順序設定への移動

- 矢印キー(`<unk> `と`) を使用して、 `Boot Maintenance Manager`を選択し、`Enter\\` を押します。

![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

- 次の画面で、 `Boot Options` を選択し、 `Enter` を押します。

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

- `Change Boot Order`を選択し、Enter\\`を押します。

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

## 2.3 ブートオーダーの変更

- 起動順序メニューに入ったら、Enterを押します。

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

- 下向きの矢印 (`<unk> `) を使用して、リストの一番下までスクロールします。
- 上に移動したいエントリを選択し、上に到達するまで「+」キーを押します。\
  ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

- 目的のブート順序が設定されたら、Enterキーを押して確認します。

## 2.4 変更の保存と適用

- 起動順序を設定した後、 `Y` を押して変更を保存します。

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

- メニューを終了し、デバイスを再起動して、新しい起動順序を適用します。

> 完了！ 完了！ 新しい注文を使用してデバイスを起動します。
> {.is-success}
> {.is-success}

