---
title: Untitled Page
description: 
published: false
date: 2025-09-20T14:07:35.377Z
tags: 
editor: markdown
dateCreated: 2025-09-20T10:44:50.776Z
---

![graphics.png](/vms/graphics.png){.align-abstopright}

Text i can write some specs here
<br>
<br>
<br>
<br>
<br>
<br>
<br>

---

# Tabs

## Board
### Tabset {.tabset}
#### Model A
Beri cool model

#### Model B
Mid tier

#### Model C
Toptier

# Dropdown

<details>
<summary><b>Title</b></summary>

Text

- Bullet
- Points

</details>

*[MIMO]: Multiple Input Multiple Output

# Abrreviations:
Please hover over MIMO
```
*[MIMO]: Multiple Input Multiple Output
```

# Tables

Normal
| Device | Status | Notes |
| -------| -------|--------|
| JMB582 based | Works   |  [Source](https://github.com/System64fumo/linux/issues/14)

Smaller: (add `{.dense}` to the end)
| Device | Status | Notes |
| -------| -------|--------|
| JMB582 based | Works   |  [Source](https://github.com/System64fumo/linux/issues/14)
{.dense}

# Math/Chemistry (Katex)

Pythagorean theorem:
$a^2 + b^2 = c^2$

Area of circle formula:
$A=πr2$


Aerobic cellular respiration:
$C_6H_{12}O_6 + 6 O_2 \;\rightarrow\; 6 CO_2 + 6 H_2O + \text{energy}$






# Graphs (Kroki)

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

# Footnotes

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

    Subsequent paragraphs are indented to show that they
belong to the previous footnote.