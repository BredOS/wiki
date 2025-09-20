---
title: 無題のページ
description:
published: false
date: 2025-09-20T14:07:35.377Z
tags:
editor: markdown
dateCreated: 2025-09-20T10:44:50.776Z
---

![graphics.png](/vms/graphics.png){.align-abstopright}

Text i can write some specs here <br> <br> <br> <br> <br> <br> <br>

---

# Tabs

## ボード

### Tabset {.tabset}

#### モデル A

Beri クールなモデル

#### モデル B

中等度

#### モデル C

Toptier

# ドロップダウン

<details><summary><b>タイトル</b></summary>

テキスト

- 弾
- 制御点

</details>

\*[MIMO]: 複数の入力

# アブラリバイバル:

MIMOの上にカーソルを合わせてください

```
*[MIMO]: 複数の入力
```

# テーブル

標準

| デバイス      | ステータス | メモ                                                        |
| --------- | ----- | --------------------------------------------------------- |
| JMB582ベース | 作品    | [Source](https://github.com/System64fumo/linux/issues/14) |

小さめ: (末尾に `{.dense}` を追加)

| デバイス                     | ステータス | メモ                                                        |
| ------------------------ | ----- | --------------------------------------------------------- |
| JMB582ベース                | 作品    | [Source](https://github.com/System64fumo/linux/issues/14) |
| {.dense} |       |                                                           |

# 数学/化学 (Katex)

ピタゴラスの定理:
$a^2 + b^2 = c^2$

円数式の面積:
$A=πr2$

好気性細胞呼吸:
$C_6H_{12}O_6 + 6 O_2 \;\rightarrow\; 6 CO_2 + 6 H_2O + \text{energy}$

# グラフ (Kroki)

```kroki
mermaid

graph TD
  A[ Anyone ] -->|Can help | B( Go to bredos.org )
  B --> C{ How to contribute? }
  C --> D[ Reporting bugs ]
  C --> E[ Sharing ideas ]
  C --> F[ Advocating ]
```

```kroki
wavedrom
{ signal: [
  { name: "clk",         wave: "p.....|..." },
  { name: "Data",        wave: "x.345x|=.x", data: ["head", "body", "tail", "data"] },
  { name: "Request",     wave: "0.1..0|1.0" },
  {},
  { name: "Acknowledge", wave: "1.....|01." }
]}
```

# 脚注:

ここでは、脚注のリファレンス、[^1]などを紹介します[^longnote]

[^1]: これが脚注です

[^longnote]: これは複数のブロックを持つものです

    後続の段落は、
    が前の脚注に属していることを示すためにインデントされます。