---
title: GRUBパスワード
description: GRUBをパスワードで保護する
published: true
date: 2025-05-05T17:13:59.940Z
tags: null
editor: markdown
dateCreated: 2025-05-05T17:13:14.153Z
---

# 🔐 GRUB パスワード保護

BredOS には、GRUBブートオプションをパスワードで制限するユーティリティが含まれています。
これにより、権限のないユーザーがデフォルト以外のエントリを起動したり、ブートパラメータを編集したりできなくなります。

# 🟢GRUBパスワードを有効にする

`sudo grub-password`

パスワードの入力と確認を求められます。
設定すると、デフォルトのGRUBエントリのみが認証なしで起動できます。

# 🔴 GRUBパスワードを無効にする

`sudo grub-password -d`

これによりパスワード制限が解除され、通常のGRUB動作が復元されます。

## メモ

設定は /etc/grub.d/99-bredos-grub-passwordに保存されます。
スクリプトはgrub-mkconfig を介して自動的に GRUB 設定を再生成します。