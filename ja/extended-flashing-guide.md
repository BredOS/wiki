---
title: 拡張フラッシュガイド
description: RKDevelopToolの使用方法についてもう少し詳しく
published: true
date: 2025-09-28T13:04:20.111Z
tags:
editor: markdown
dateCreated: 2025-09-28T13:02:13.948Z
---

人生でもっとプログレスバーが欲しいだけですよね？
:thumbsup: は心配しないでください。

## 選択したフラッシュメディア情報を読み込み中

- `sudo rkdeveloptool rfi`

このコマンドは、選択したフラッシュメディアの詳細を表示します。
デフォルトでは、これは通常、利用できない場合を除き、eMMCです。

```
[bill88t@prion | ~/Downloads]> sudo rkdeveloptool rfi
Flash Info:
	Manufacturer: SAMSUNG, value=00
	Flash Size: 14910 MB
	Flash Size: 30535680 Sectors
	Block Size: 512 KB
	Page Size: 2 KB
	ECC Bits: 0
	Access Time: 40
	Flash CS: Flash<0>
```

## フラッシュターゲットの変更

フラッシュ/ないeMMCではなく別のことをダンプしたいですか?

- SDカードを選択するには `sudo rkdeveloptool cs 2` 。
- `sudo rkdeveloptool cs 9` で SPINOR チップを選択します。
- `sudo rkdeveloptool cs 1` で再びeMMCを選択します。

変更は `sudo rkdeveloptool rfi` に反映されます。