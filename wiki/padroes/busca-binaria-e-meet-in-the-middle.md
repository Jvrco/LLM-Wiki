---
titulo: Busca Binária e Meet in the Middle
tipo: padrao
tags: [busca-binaria, meet-in-the-middle, two-pointers, lower-bound]
fontes:
  - raw/Competitive-Programming-Lib/Library/Buscas/bs1.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/bs2.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/BB.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/MeetInTheMiddle.cpp
  - raw/Competitive-Programming-Lib/Library/Buscas/MM.cpp
  - raw/Competitive-Programming-Lib/Library/Others/cows.cpp
  - raw/Competitive-Programming-Lib/Library/Others/prefixsum.cpp
  - raw/Competitive-Programming-Lib/Library/DP/IncreasingSubsequence.cpp
atualizado: 2026-11-25
---

# Busca Binária e Meet in the Middle

Esta página conecta técnicas de busca que no repositório bruto ficaram espalhadas entre `Buscas/`, `Others/` e `DP/`.

---

## 1. Os 3 Padrões de Busca Binária na Lib

### A. Busca Binária por Invariante (`Buscas/bs1.cpp`)
- Mantém `l` sempre válido (`a[l] <= x`) e `r` sempre inválido (`a[r] > x`), começando fora dos limites: `l = -1, r = n`.
- Loop: `while (r > l + 1)` — **imune a loop infinito** e dispensa variável `ans` separada.
- Resultado: `l + 1` é a quantidade de elementos $\le x$ (equivalente a `upper_bound(a, a+n, x) - a`).

### B. Busca Binária na Resposta — Minimização (`Buscas/bs2.cpp`, `Buscas/BB.cpp`)
- Procura o **menor** `m` tal que `check(m) == true`.
- Padrão:
  ```cpp
  while (l <= r) {
      ll m = l + (r - l) / 2;
      if (check(m)) { ans = m; r = m - 1; }
      else { l = m + 1; }
  }
  ```
- **Atenção:** sempre inicialize `ans` (ex.: `ll ans = -1;`) e garanta `r` com folga em `ll` (ver bug `int r = 1e7` em `Buscas/BB.cpp`).

### C. Busca Binária na Resposta — Maximização (`Others/cows.cpp`)
- Procura o **maior** `mid` tal que `check(mid) == true` (ex.: SPOJ *AGGRCOW* — maximizar a distância mínima).
- Padrão invertido: se `check(mid)` é verdadeiro, `ans = mid; l = mid + 1;`; caso contrário, `r = mid - 1;`.
- **Atenção:** em `Others/cows.cpp`, `mid` foi declarado como `int` apesar de `l, r` serem `ll` — sempre use `ll mid = l + (r - l) / 2;`.

### D. Busca Binária via STL (`lower_bound` / `upper_bound`)
Aparece integrada a outras técnicas na lib:
- `DP/IncreasingSubsequence.cpp`: `lower_bound` para manter o menor final de subsequência crescente de cada tamanho (LIS em $O(n \log n)$).
- `Others/prefixsum.cpp`: `upper_bound` sobre valores únicos `w[]` para pular em blocos todos os elementos absorvíveis de uma vez.
- `Range/segtreewithcompression.cpp`: `lower_bound` e `upper_bound` para mapear valores reais em índices comprimidos.
- `Buscas/MM.cpp`: `lower_bound(sub2.begin(), sub2.end(), m - x)` para achar o complemento ótimo mod $m$.

---

## 2. Meet in the Middle ($n \le 40$)

Quando $n \approx 36 \dots 40$, a força bruta $O(2^n)$ dá TLE, mas dividir o vetor em duas metades (`left` e `right`) de tamanho $\le 20$ gera no máximo $2^{20} \approx 10^6$ somas por lado:

| Variante | Arquivo | Como combina `sub1` e `sub2` |
|---|---|---|
| **Contar subconjuntos com soma exata $x$** | `Buscas/MeetInTheMiddle.cpp` | Ordena ambos e usa *two pointers* (`i` sobe em `sub1`, `j` desce em `sub2`), multiplicando blocos de elementos iguais. |
| **Maximizar soma módulo $m$** | `Buscas/MM.cpp` | Ordena apenas `sub2`; para cada `x` em `sub1`, busca `it = lower_bound(sub2, m - x)` e testa `--it` (melhor soma $< m$ sem dar volta). |

---

## Páginas Relacionadas

- [[wiki/categorias/buscas|Buscas]]
- [[wiki/categorias/outros|Outros]]
- [[wiki/categorias/dp|Programação Dinâmica (DP)]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
