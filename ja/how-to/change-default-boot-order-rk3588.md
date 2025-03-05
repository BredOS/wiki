---
title: RK3588のデフォルトブートオーダーを変更する方法
description: UEFIファームウェア設定を使用して、RK3588ベースのデバイスでデフォルトの起動順序を変更する方法を学びます。
published: true
date: 2025-02-23T15:45:23.760Z
tags: null
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 🔄 RK3588 デバイスのデフォルトブート順序の変更

BredOS を実行している RK3588 ベースのデバイスでブート順序を変更する必要がある場合は、次の手順に従います。

---

## 🔹 UEFI ブートメニューへのアクセス

1. \*\*デバイスの電源を入れて、起動中に **BredOS のロゴ** が表示されるのを待ちます。
2. **ESCキーを1回押すと**ロゴが表示されます。UEFIメニューに入ります。

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

---

## 🛠️ ブート順序設定へ移動

1. **ブートメンテナンスマネージャー**を選択するには、**矢印キー(`<unk> `と\`)**を使用して**Enter**を押します。\
  ![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

2. 次の画面で**ブートオプション**を選択し、**Enter**を押します。

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

3. **起動順序を変更**を選択し、**Enter**を押します。

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

---

## 🔧 ブートオーダーを変更する

1. 一度ブート順序メニューの中で、**Enter** を押します。

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

2. \*\*下向き矢印(`<unk> `)\*\*を使ってリストの一番下までスクロールします。

3. 上に移動したいエントリを選択し、**`+`キー**を上に到達するまで押します。\
  ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

4. 目的のブート順序が設定されたら、**Enter** を押して確認します。

---

## 💾 変更を保存して適用する

1. 起動順序を設定した後、 **`Y`** を押して変更を保存します。

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

2. メニューを終了して **デバイスを再起動** して、新しい起動順序を適用します。

---

✅ **完了！** 新しい順序でデバイスが起動します。 🚀
