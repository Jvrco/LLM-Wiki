---
titulo: Checklist Pré-Contest (Caderno PDF e Correções)
tipo: auditoria
tags: [auditoria, checklist, contest, pdf, query-writeback]
fontes:
  - raw/Competitive-Programming-Lib/contents.txt
  - wiki/auditoria/lint-inicial.md
atualizado: 2026-11-25
---

# Checklist Pré-Contest (Caderno PDF e Correções)

> Página gerada por operação **`query` com *write-back*** consolidando as ações prioritárias antes de imprimir o caderno via `generate_pdf.py` ou reutilizar templates em maratona.

---

## 1. Correções Críticas nos Templates (Prioridade 1)

- [ ] `TeoriaDosNumeros/relations.cpp`: corrigir identidade de Pascal para $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$.
- [ ] `Grafos/BFS.cpp`: remover `freopen("jumping.in", "r", stdin);`.
- [ ] `Strings/Hash.cpp`, `Hash2.cpp`, `Hash3.cpp`: trocar `s[i] - 'a'` por `(s[i] - 'a' + 1)` e usar `mod_mul` no pré-cálculo de `pref[]` e `powers[]`.
- [ ] `Geometria/ConvexHull.cpp`: trocar `double v = AB.cross(BC);` por `ll v = AB.cross(BC);`.
- [ ] `Others/prefixsum2.cpp`: inicializar `ll prefix[MAXN+1] = {0};`.
- [ ] `Others/cows.cpp`: trocar `int mid = (l+r)/2;` por `ll mid = l + (r - l) / 2;`.
- [ ] `DP/CountingNumber.cpp`: tratar $a = 0$ e evitar escrita em `dp[n][-1]`.
- [ ] `TeoriaDosNumeros/fastexp.cpp`: adicionar `a %= m;` antes do loop em `fexp`.

---

## 2. Sincronizar `contents.txt` para o PDF do Caderno (Prioridade 2)

Atualmente **37 dos 64 arquivos** ficam fora do PDF. Incluir no `contents.txt`:
- [ ] Nova seção `[DP]` (prioridade: `IncreasingSubsequence.cpp`, `Knapsack.cpp`, `LCS.cpp`, `CountingNumber.cpp`, `SumofDigits.cpp`, `DpGridPaths.cpp`).
- [ ] Nova seção `[Strings]` (`Hash.cpp`, `Trie.cpp`, `TrieXorMin.cpp`).
- [ ] Completar `[Range Query]` com `segLazy.cpp`, `segtreewithcompression.cpp`, `listremoval.cpp`, `Pqueries.cpp`, `RangeUpdateQueries` (renomear para `.cpp`) e `Range Xor Queries` (renomear para `RangeXorQueries.cpp`).
- [ ] Completar `[Teoria dos numeros]` com `fastexp.cpp`, `matrixexp.cpp`, `commondivisors.cpp`.

---

## 3. Padronização Opcional (Prioridade 3)

- [ ] Trocar `const ll INF = LLONG_MAX;` por `const ll INF = 1e18;` nos arquivos de grafos/range para evitar overflow em `INF + w`.
- [ ] Remover globais não utilizadas (`visited[MAXV]`, `adj[MAXV]`, `dx/dy`) de templates de SegTree, DSU e Geometria para economizar páginas no caderno impresso.

---

## Páginas Relacionadas

- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
