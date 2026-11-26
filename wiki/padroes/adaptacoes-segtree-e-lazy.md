---
titulo: "Adaptações de Segment Tree e Lazy Propagation"
tipo: padrao
tags: [range-queries, segtree, lazy-propagation, adaptacao, query-writeback]
fontes:
  - raw/Competitive-Programming-Lib/Library/Range/segLazy.cpp
  - raw/Competitive-Programming-Lib/Library/Range/segtree.cpp
  - raw/Competitive-Programming-Lib/Library/Range/segtreewithcompression.cpp
atualizado: 2026-11-25
---

# Adaptações de Segment Tree e Lazy Propagation

> Página gerada por operação **`query` com *write-back***: em vez de recalcular essa adaptação em toda sessão futura, ela fica compilada permanentemente na wiki.

Na lib bruta, `Range/segLazy.cpp` implementa apenas **Range Add + Range Min** (1-based). Abaixo estão as 3 adaptações mais comuns em contests e os pontos exatos onde a lógica muda.

---

## 1. De Range Min para Range Sum (`segLazy.cpp`)

Apenas **4 pontos** precisam mudar em `Range/segLazy.cpp`:

1. **Merge (`build` e `update`):**
   - De: `seg[node] = min(seg[2 * node], seg[2 * node + 1]);`
   - Para: `seg[node] = seg[2 * node] + seg[2 * node + 1];`
2. **Propagação (`push`):**
   - De: `seg[node] += lazy[node];`
   - Para: `seg[node] += lazy[node] * (end - start + 1);` *(armadilha clássica: esquecer de multiplicar pelo tamanho do intervalo!)*
3. **Elemento neutro (`rangem` / `query`):**
   - De: `if (r < start || end < l) return INF;`
   - Para: `if (r < start || end < l) return 0LL;`
4. **Retorno da query:**
   - De: `return min(lm, rm);`
   - Para: `return lm + rm;`

---

## 2. De Range Add para Range Assign (setar intervalo para `val`)

Quando a atualização é *"troque todos os elementos de $[l, r]$ por $v$"* (em vez de somar $+v$):
- Um `lazy[node] == 0` pode significar *"atribuir 0"* ou *"nada pendente"*.
- **Solução:** adicione um vetor `vector<bool> hasLazy(4 * n + 5, false);` (ou use um sentinela fora do domínio, como `LLONG_MIN`).
- Em `push`:
  - Para **min/max**: `seg[node] = lazy[node];`
  - Para **soma**: `seg[node] = lazy[node] * (end - start + 1);`
  - Nos filhos: `lazy[2*node] = lazy[node]; hasLazy[2*node] = true;` (sobrescreve, **não** soma!).

---

## 3. Atenção ao Misturar `segtree.cpp` e `segtreewithcompression.cpp`

| Detalhe | `segtree.cpp` / `segLazy.cpp` | `segtreewithcompression.cpp` |
|---|---|---|
| Raiz da árvore | `node = 1` | `node = 0` |
| Intervalo inicial | `[1, n]` | `[0, num - 1]` |
| Filhos | `2 * node` e `2 * node + 1` | `2 * node + 1` e `2 * node + 2` |
| Tipo padrão | `int` (`segtree.cpp`) / `ll` (`segLazy.cpp`) | `ll` |

**Regra prática:** ao combinar Compressão de Coordenadas com Lazy Propagation, mantenha **toda** a árvore 0-based (como `segtreewithcompression.cpp`) ou mapeie o índice comprimido com `+ 1` (`lower_bound(...) - comp.begin() + 1`) para continuar usando o padrão 1-based de `segLazy.cpp`.

---

## Páginas Relacionadas

- [[wiki/padroes/guia-de-decisao-range-queries|Guia de Decisão: Range Queries]]
- [[wiki/categorias/range-queries|Range Queries]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
