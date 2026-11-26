---
titulo: "Guia de Decisão: Range Queries"
tipo: padrao
tags: [range-queries, decisao, segtree, fenwick, lazy, prefix-sum]
fontes:
  - raw/Competitive-Programming-Lib/Library/Range/PrefixSum2d.cpp
  - raw/Competitive-Programming-Lib/Library/Range/Fenwicktree.cpp
  - raw/Competitive-Programming-Lib/Library/Range/RangeUpdateQueries
  - raw/Competitive-Programming-Lib/Library/Range/segtree.cpp
  - raw/Competitive-Programming-Lib/Library/Range/Range Xor Queries
  - raw/Competitive-Programming-Lib/Library/Range/segLazy.cpp
  - raw/Competitive-Programming-Lib/Library/Range/listremoval.cpp
  - raw/Competitive-Programming-Lib/Library/Range/Pqueries.cpp
  - raw/Competitive-Programming-Lib/Library/Range/segtreewithcompression.cpp
  - raw/Competitive-Programming-Lib/Library/Others/prefixsum.cpp
  - raw/Competitive-Programming-Lib/Library/Others/prefixsum2.cpp
  - raw/Competitive-Programming-Lib/Library/Others/suffixsum.cpp
atualizado: 2026-11-25
---

# Guia de Decisão: Range Queries

Síntese transversal conectando todos os arquivos de `Library/Range/` e os prefix/suffix sums em `Library/Others/`. Use esta tabela durante treinos e contests para escolher imediatamente o arquivo certo da lib.

---

## Matriz de Escolha Rápida

| Cenário do Problema | Estrutura Ideal na Lib | Arquivo | Complexidade (Update / Query) |
|---|---|---|---|
| **Estático 1D** (soma, XOR) | Prefix Sum / Suffix Sum | `Others/prefixsum2.cpp`, `Others/suffixsum.cpp` | — / $O(1)$ |
| **Estático 2D** (soma em submatriz) | Prefix Sum 2D (inclusão-exclusão) | `Range/PrefixSum2d.cpp` | — / $O(1)$ |
| **Point update + Range sum** | Fenwick Tree (BIT) | `Range/Fenwicktree.cpp` | $O(\log n)$ / $O(\log n)$ |
| **Range add + Point query** | Fenwick Tree + Difference Array | `Range/RangeUpdateQueries` | $O(\log n)$ / $O(\log n)$ |
| **Point update + Range min/max/gcd** | Segment Tree recursiva | `Range/segtree.cpp` | $O(\log n)$ / $O(\log n)$ |
| **Point update + Range XOR** | Segment Tree de XOR | `Range/Range Xor Queries` | $O(\log n)$ / $O(\log n)$ |
| **Range add + Range min** | Segment Tree com Lazy Propagation | `Range/segLazy.cpp` | $O(\log n)$ / $O(\log n)$ |
| **$k$-ésimo elemento ativo + remoção** | SegTree com busca na árvore (`find`) | `Range/listremoval.cpp` | $O(\log n)$ / $O(\log n)$ |
| **Minimizar $p_i + |i - k|$ com update** | Duas SegTrees (`arr[i]+i` e `arr[i]-i`) | `Range/Pqueries.cpp` | $O(\log n)$ / $O(\log n)$ |
| **Valores grandes ($\le 10^9$) + range count** | SegTree + Compressão de Coordenadas | `Range/segtreewithcompression.cpp` | $O(\log Q)$ / $O(\log Q)$ |

---

## Adaptações Frequentes dos Templates da Lib

1. **Transformar `segLazy.cpp` (Range Add + Range Min) em Range Add + Range Sum:**
   - Em `build` e `update`: troque `min(seg[2*node], seg[2*node+1])` por `seg[2*node] + seg[2*node+1]`.
   - Em `push`: troque `seg[node] += lazy[node];` por **`seg[node] += lazy[node] * (end - start + 1);`**.
   - Em `rangem`: troque o elemento neutro `INF` por `0LL` e `min(lm, rm)` por `lm + rm`.
2. **Transformar `segtree.cpp` de `int` para `long long`:**
   - Troque `vector<int>` por `vector<ll>` e `INT_MAX` por `INF` (de preferência `1e18`).
3. **Atenção à indexação ao misturar arquivos:**
   - Todos os templates de `Range/` são **1-based**, **exceto** `segtreewithcompression.cpp`, que é **0-based** (`build(0, 0, num-1, arr)` com filhos `2*node+1` e `2*node+2`).

---

## Páginas Relacionadas

- [[wiki/categorias/range-queries|Range Queries]]
- [[wiki/categorias/outros|Outros]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
