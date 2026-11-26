---
titulo: Buscas
tipo: categoria
tags: [buscas, busca-binaria, meet-in-the-middle, backtracking]
fontes:
  - raw/Competitive-Programming-Lib/Library/Buscas/BB.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/bs1.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/bs2.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/MeetInTheMiddle.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/MM.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/Queens.cpp
atualizado: 2026-11-25
---

# Buscas

Mapa compilado da pasta `Library/Buscas/` (6 arquivos). Cobre três famílias de técnicas: **Busca Binária** (em vetor e na resposta), **Meet in the Middle** ($n \le 40$) e **Backtracking**.

> **Conexões fora desta pasta:** veja também `Others/cows.cpp` (busca binária na resposta — SPOJ AGGRCOW) e `Grafos/backtrack.dfs.cpp` (backtracking de permutação). Síntese completa em [[wiki/padroes/busca-binaria-e-meet-in-the-middle|Busca Binária e Meet in the Middle]].

---

## Inventário

| Arquivo | Tipo | Técnica / Problema | Complexidade | No `contents.txt`? |
|---|---|---|---|---|
| `Buscas/bs1.cpp` | Template | Busca binária por invariante (`l = -1, r = n`, `while (r > l + 1)`): conta elementos $\le x$. | $O((n + q) \log n)$ | Sim |
| `Buscas/bs2.cpp` | Template | Busca binária na resposta clássica (`while (l <= r)`), encontra menor $m$ que satisfaz `isPos(m, s)`. | $O(\log R \cdot T_{\text{check}})$ | Sim |
| `Buscas/BB.cpp` | Problema | Busca binária na resposta (Codeforces *Robin Hood in Town*): mínimo $m$ adicionado ao maior elemento para que a média $/ 2 > a_{\lfloor n/2 \rfloor}$. | $O(n \log n + \log R)$ | **Não** |
| `Buscas/MeetInTheMiddle.cpp` | Template / Problema | Meet in the Middle (CSES *Meet in the Middle*): conta subconjuntos com soma exata $x$ usando *two pointers* com multiplicidades. | $O(2^{n/2} \log 2^{n/2})$ | Sim |
| `Buscas/MM.cpp` | Problema | Meet in the Middle modular (Codeforces 888E *Maximum Subsequence*): maior soma de subconjunto módulo $m$ usando `lower_bound`. | $O(2^{n/2} \log 2^{n/2})$ | **Não** |
| `Buscas/Queens.cpp` | Problema | Backtracking das 8 Rainhas com obstáculos `'*'` (CSES *Chessboard and Queens*), marcando colunas e diagonais (`r + col` e `r - col + 7`). | $O(N!)$ com poda | Sim |

---

## Detalhes e Armadilhas (*Gotchas*)

- **`BB.cpp` — Limite superior `r = 1e7` insuficiente:** `int r = 1e7;` pode falhar quando $a_i$ é grande (em *Robin Hood in Town*, $m$ pode chegar a $10^{12}$). Além disso, usa ponto flutuante `(double)(contador + m) / (2.0 * n) > a[n/2]`; prefira aritmética inteira: `contador + m > 2LL * n * a[n/2]`. Ver [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]].
- **`bs1.cpp`, `bs2.cpp`, `MeetInTheMiddle.cpp`:** são snippets no estilo `void solve()` **sem `int main()`**. Em `bs2.cpp`, `ans` não é inicializado (se `isPos` nunca for verdadeiro, imprime lixo).
- **`MeetInTheMiddle.cpp` vs. `MM.cpp`:**
  - `MeetInTheMiddle.cpp` ordena ambas as metades (`sub1` e `sub2`) e usa *two pointers* para contar multiplicidades em $O(|sub1| + |sub2|)$.
  - `MM.cpp` ordena apenas `sub2` e faz `lower_bound(m - x)` para cada `x` em `sub1` (com `--it` para achar o maior elemento $< m - x$).
- **`Queens.cpp`:** o truque de indexação de diagonais `diag1[r + col]` (tamanho $2N - 1$) e `diag2[r - col + (N - 1)]` é reutilizável para qualquer problema de $N$-Rainhas.

---

## Páginas Relacionadas

- [[wiki/padroes/busca-binaria-e-meet-in-the-middle|Busca Binária e Meet in the Middle]]
- [[wiki/categorias/outros|Outros]] (contém `cows.cpp` e `prefixsum.cpp` com busca binária)
- [[wiki/categorias/grafos|Grafos]] (contém `backtrack.dfs.cpp`)
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
