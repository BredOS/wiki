---
title: Página sin título
description:
published: false
date: 2025-09-20T15:21:38.301Z
tags:
editor: markdown
dateCreated: 2025-09-20T10:44:50.776Z
---

![graphics.png](/vms/graphics.png =25%x){.align-right}

El texto puede escribir algunas especificaciones aquí <br>format@@2<br> <br> <br> <br> <br> <br> <br> <br> <br> <br>

---

# Tabs

## Tablero

### Tabset {.tabset}

#### Modelo A

Modelo fresco Beri

#### Modelo B

Nivel medio

#### Modelo C

Toptier

# Soltar

<details><summary><b>Título</b></summary>

Texto

- Bala
- Puntos

</details>

\*[MIMO]: Múltiples entradas de salida

# Notas al pie

Aquí hay una referencia a pie de página,[^1] y otra.[^longnote]

# Abrreviaciones:

Por favor pase el cursor sobre MIMO

```
*[MIMO]: Múltiples entradas de salida
```

# Tablas

Normal

| Dispositivo      | Estado | Notas                                                     |
| ---------------- | ------ | --------------------------------------------------------- |
| Basado en JMB582 | Obras  | [Source](https://github.com/System64fumo/linux/issues/14) |

Más pequeño: (añade `{.dense}` al final)

| Dispositivo              | Estado | Notas                                                     |
| ------------------------ | ------ | --------------------------------------------------------- |
| Basado en JMB582         | Obras  | [Source](https://github.com/System64fumo/linux/issues/14) |
| {.dense} |        |                                                           |

# listas

Algunas cosas:

- Elemento de cuadrcula 1
- Elemento de cuadrícula 2
- Artículo cuadrícula 3
  {.grid-list}

Herramienta muy

- [Lorem ipsum dolor sit amet _Subtitle description here_](https://www.google.com)
- [Elit adipiscina consecetur _Otra descripción de subtítulos aquí_](https://www.google.com)
- [Morbi vehicula aliquam _Third subtitle description here_](https://www.google.com)
  {.links-list}

# Teclas del teclado

Pulsa <kbd>F</kbd> para respetar

# Matemática/Química (Katex)

Teorema pitágoro:
$a^2 + b^2 = c^2$

Área de la fórmula del círculo:
$A=πr2$

Respiración celular aeróbica:

$$
C_6H_{12}O_6 + 6 O_2 \;\rflecha de flujo\; 6 CO_2 + 6 H_2O + \text{energy}
$$

# Gráficas (Kroki)

```kroki
sirena

gráfica TD
  A[ Cualquiera ] -->|Puede ayudar | B( Ir a bredos. rg )
  B --> C{ ¿Cómo contribuir? }
  C --> D[ Reportando errores ]
  C --> E [ Compartir ideas ]
  C --> F[ Provocar ]
```

<br>

```kroki
wavedrom
{ signal: [
  { name: "clk", onda: "p. ...|..." },
  { name: "Data", onda: "x.345x|=. ", data: ["head", "body", "tail", "data"] },
  { name: "Request", onda: "0.1..0|1. " },
  {},
  { name: "Reconocimiento", onda: "1.....|01." }
]}
```

[^1]: Esta es la nota al pie.

[^longnote]: Aquí hay uno con múltiples bloques.

    Los párrafos posteriores están sangrados para mostrar que
    pertenecen a la nota anterior al pie de página.