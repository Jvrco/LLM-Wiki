---
titulo: Range Queries
tipo: categoria
tags: [range-queries, segtree, fenwick, lazy-propagation, prefix-sum-2d, compressao-coordenadas]
fontes:
  - raw/Competitive-Programming-Lib/Library/Range/Fenwicktree.cpp
  - raw/Competitive-Programming-Lib/Library/Range/listremoval.cpp
  - raw/Competitive-Programming-Lib/Library/Range/Pqueries.cpp
  - raw/Competitive-Programming-Lib/Library/Range/PrefixSum2d.cpp
  - raw/Competitive-Programming-Lib/Library/Range/Range Xor Queries
  - raw/Competitive-Programming-Lib/Library/Range/RangeUpdateQueries
  - raw/Competitive-Programming-Lib/Library/Range/segLazy.cpp
  - raw/Competitive-Programming-Lib/Library/Range/segtree.cpp
  - raw/Competitive-Programming-Lib/Library/Range/segtreewithcompression.cpp
atualizado: 2026-11-25
---

# Range Queries

Mapa compilado da pasta `Library/Range/` (9 arquivos). Apenas 3 deles (`Fenwicktree.cpp`, `PrefixSum2d.cpp`, `segtree.cpp`) estão no `contents.txt`.

> **Guia prático de escolha:** consulte [[wiki/padroes/guia-de-decisao-range-queries|Guia de Decisão: Range Queries]] para decidir rapidamente qual estrutura usar num problema.

---

## Inventário

| Arquivo | Tipo | Estrutura / Operações | Indexação | No `contents.txt`? |
|---|---|---|---|---|
| `Range/PrefixSum2d.cpp` | Template | **Prefix Sum 2D** estático: soma em submatriz $(x_1, y_1) \dots (x_2, y_2)$ em $O(1)$ (CSES *Forest Queries*). | 1-based | Sim |
| `Range/Fenwicktree.cpp` | Template | **Fenwick Tree (BIT)** clássica: point set/add + range sum $[a, b]$ em $O(\log n)$ (CSES *Dynamic Range Sum Queries*). | 1-based | Sim |
| `Range/RangeUpdateQueries` *(sem `.cpp`)* | Template / Problema | **Fenwick Tree como Difference Array**: range add $[a, b] + u$ + point query em $k$ (CSES *Range Update Queries*). | 1-based | **Não** |
| `Range/segtree.cpp` | Template | **Segment Tree** recursiva: point set + range min $[a, b]$ em $O(\log n)$ (CSES *Dynamic Range Minimum Queries*). | 1-based (`2*node`) | Sim |
| `Range/Range Xor Queries` *(sem `.cpp`)* | Template / Problema | **Segment Tree de XOR**: point set + range XOR $[a, b]$ (CSES *Range Xor Queries*). | 1-based (`2*node`) | **Não** |
| `Range/segLazy.cpp` | Template | **Segment Tree com Lazy Propagation**: range add $[l, r] + \text{val}$ + range min $[l, r]$ em $O(\log n)$. | 1-based (`2*node`) | **Não** |
| `Range/listremoval.cpp` | Template / Problema | **Segment Tree com busca binária na árvore (`find`)**: encontra e remove o $k$-ésimo elemento vivo em $O(\log n)$ (CSES *List Removals*). | 1-based (`2*node`) | **Não** |
| `Range/Pqueries.cpp` | Problema | **Duas Segment Trees simultâneas** (`arr[i] + i` e `arr[i] - i`) para minimizar $p_i + |i - k|$ com point update (CSES *Pizzeria Queries*). | 1-based (`2*node`) | **Não** |
| `Range/segtreewithcompression.cpp` | Template / Problema | **Segment Tree + Compressão de Coordenadas offline**: conta valores no intervalo $[a, b]$ com point updates (CSES *Salary Queries*). | **0-based** (`2*node+1`) | **Não** |

---

## Detalhes e Armadilhas (*Gotchas*)

- **Inconsistência de indexação na SegTree:** 6 arquivos de SegTree usam raiz `1`, filhos `2*node` / `2*node+1` e intervalo `[1, n]`. **Exceção:** `segtreewithcompression.cpp` usa raiz `0`, filhos `2*node+1` / `2*node+2` e intervalo `[0, num-1]` (e é snippet `solve()` sem `main()`).
- **Arquivos sem extensão `.cpp`:** `Range Xor Queries` (inclusive com espaços no nome!) e `RangeUpdateQueries` não possuem extensão `.cpp`, o que pode quebrar scripts de compilação ou o gerador de PDF.
- **Adaptando `segLazy.cpp` de Range Min para Range Sum:** atenção! Na linha 483, `seg[node] += lazy[node];` só funciona para **min/max**. Para **range sum**, é obrigatório multiplicar pelo tamanho do intervalo: `seg[node] += lazy[node] * (end - start + 1);`.
- **`segtree.cpp` usa `int`:** se os valores passarem de $2 \times 10^9$ ou se adaptar para **soma**, troque `vector<int>` e `INT_MAX` por `vector<ll>` e `INF`.
- **XOR estático vs. dinâmico:** `Range Xor Queries` usa uma SegTree completa de $4n$, mas para queries estáticas sem update um simples `prefix_xor[r] ^ prefix_xor[l-1]` resolve em $O(1)$. A SegTree já traz `update()` pronto caso o problema seja dinâmico.

---

## Páginas Relacionadas

- [[wiki/padroes/guia-de-decisao-range-queries|Guia de Decisão: Range Queries]]
- [[wiki/categorias/outros|Outros]] (contém `prefixsum.cpp`, `prefixsum2.cpp`, `suffixsum.cpp`)
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
