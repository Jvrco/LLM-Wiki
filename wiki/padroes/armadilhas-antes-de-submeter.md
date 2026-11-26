---
titulo: Armadilhas Antes de Submeter (Checklist da Lib)
tipo: padrao
tags: [debugging, armadilhas, checklist, contest, query-writeback]
fontes:
  - wiki/auditoria/lint-inicial.md
  - wiki/padroes/conventions-e-estilos-da-lib.md
  - raw/notas/erros-comuns-contest.md
atualizado: 2026-11-26
---

# Armadilhas Antes de Submeter (Checklist da Lib)

> Página gerada por **`query` com *write-back*** + **`ingest`** de `raw/notas/erros-comuns-contest.md`. Resume os erros recorrentes específicos dos templates desta biblioteca para checar em 30 segundos antes de submeter.

---

## 1. I/O e Template Base
- [ ] **Sem `freopen` perdido:** `Grafos/BFS.cpp` tem `freopen("jumping.in", "r", stdin);` hardcoded.
- [ ] **Quebra de linha rápida:** nos arquivos do Estilo B (`#define endll '\n'`), o corpo do código ainda chama `endl` (que dá flush!). Em problemas com $10^5+$ linhas de saída, troque por `'\n'`.
- [ ] **Tem `int main()`?** Mais de 20 arquivos da lib (`bs1`, `bs2`, `ConvexHull`, `Hash*`, `Dp*`, `Toposort`, etc.) só definem `void solve()`.

## 2. Overflow e Tipos Numéricos
- [ ] **`INF = 1e18`, nunca `LLONG_MAX` em somas:** vários arquivos de grafos/range usam `LLONG_MAX`; somar qualquer peso `w` gera overflow assinado.
- [ ] **Busca binária em `ll`:** nunca declare `int mid` quando `l, r` são `ll` (bug encontrado em `Others/cows.cpp`) e cheque se `r` cobre o pior caso (`Buscas/BB.cpp` usa `r = 1e7`).
- [ ] **Geometria inteira:** mantenha o produto vetorial em `ll` (nunca `double`, como ocorre em `Geometria/ConvexHull.cpp`).
- [ ] **Exponenciação rápida:** garanta `a %= m;` antes do loop (`TeoriaDosNumeros/fastexp.cpp` omite isso).

## 3. Estruturas de Dados e Strings
- [ ] **Indexação da SegTree:** 1-based em quase toda `Range/`, **exceto** `segtreewithcompression.cpp` (0-based). Ver [[wiki/padroes/adaptacoes-segtree-e-lazy|Adaptações de Segment Tree e Lazy Propagation]].
- [ ] **Lazy Propagation para soma:** em `push()`, multiplique `lazy[node] * (end - start + 1)`.
- [ ] **Rolling Hash (`Hash*.cpp`):** troque `s[i] - 'a'` por `(s[i] - 'a' + 1)` e use `mod_mul` no pré-cálculo.
- [ ] **Array local na stack:** sempre inicialize `prefix[0] = 0` (bug em `Others/prefixsum2.cpp`).

## 4. Casos Limite (Edge Cases)
- [ ] **Digit DP com $a = 0$:** trate `a == 0` antes de chamar `solve(a - 1)` (`DP/CountingNumber.cpp`).
- [ ] **Grid DFS/BFS:** valide a célula inicial (`Grafos/DFS.cpp` não testa `grid[0][0] == 's'`).
- [ ] **Dijkstra com cupom (`dijestados2.cpp`):** use `min(dist[n][0], dist[n][1])` no caso de $n = 1$ ou caminho ótimo sem cupom.

---

## Páginas Relacionadas

- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/auditoria/checklist-pre-contest|Checklist Pré-Contest (Caderno PDF e Correções)]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
