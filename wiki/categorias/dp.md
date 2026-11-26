---
titulo: Programação Dinâmica (DP)
tipo: categoria
tags: [dp, knapsack, digit-dp, lis, lcs, grid-dp]
fontes:
  - raw/Competitive-Programming-Lib/Library/DP/CountingNumber.cpp
  - raw/Competitive-Programming-Lib/Library/DP/Dp1.cpp
  - raw/Competitive-Programming-Lib/Library/DP/Dp2.cpp
  - raw/Competitive-Programming-Lib/Library/DP/DpGridPaths.cpp
  - raw/Competitive-Programming-Lib/Library/DP/DpJump.cpp
  - raw/Competitive-Programming-Lib/Library/DP/IncreasingSubsequence.cpp
  - raw/Competitive-Programming-Lib/Library/DP/Knapsack.cpp
  - raw/Competitive-Programming-Lib/Library/DP/Knapsack2.cpp
  - raw/Competitive-Programming-Lib/Library/DP/LCS.cpp
  - raw/Competitive-Programming-Lib/Library/DP/rectangularcutting.cpp
  - raw/Competitive-Programming-Lib/Library/DP/SumofDigits.cpp
atualizado: 2026-11-25
---

# Programação Dinâmica (DP)

Mapa compilado da pasta `Library/DP/` (11 arquivos). **Atenção:** nenhum destes 11 arquivos está listado no `contents.txt` atual da lib (ver [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]).

Síntese de padrões e transições em [[wiki/padroes/dp-classicos-e-digit-dp|DP Clássicos e Digit DP]].

---

## Inventário

| Arquivo | Tipo | Problema / Algoritmo | Abordagem | Complexidade |
|---|---|---|---|---|
| `DP/Dp1.cpp` | Problema / Template | Mínimo de moedas para soma $x$ (CSES *Minimizing Coins*). | Bottom-up 1D | $O(n \cdot x)$ |
| `DP/Dp2.cpp` | Problema | Mínimo de passos removendo um dígito até chegar a 0 (CSES *Removing Digits*). | Bottom-up 1D | $O(n \log_{10} n)$ |
| `DP/DpGridPaths.cpp` | Problema / Template | Contagem de caminhos em grid $n \times n$ evitando `'*'` mod $10^9+7$ (CSES *Grid Paths*). | Bottom-up 2D | $O(n^2)$ |
| `DP/DpJump.cpp` | Problema | Custo mínimo pulando até $k$ posições com custo $|h_i - h_{i-j}|$ (AtCoder *Frog 2*). | Top-down memo | $O(n \cdot k)$ |
| `DP/IncreasingSubsequence.cpp` | Template | Longest Increasing Subsequence (LIS estrita) usando `lower_bound` (CSES *Increasing Subsequence*). | Greedy + BS | $O(n \log n)$ |
| `DP/Knapsack.cpp` | Template | Mochila 0/1 ($n \le 100, W \le 10^5$, AtCoder *Knapsack 1*). | Top-down 2D | $O(n \cdot W)$ |
| `DP/Knapsack2.cpp` | Problema | Mochila ilimitada com agrupamento de itens de mesmo tamanho (mantém apenas maior valor por `s.size()`). | Bottom-up 1D | $O(W \cdot D)$ |
| `DP/LCS.cpp` | Template | Longest Common Subsequence + **reconstrução da string** via função `r(i, j)` (AtCoder *LCS*). | Top-down 2D | $O(|s| \cdot |t|)$ |
| `DP/rectangularcutting.cpp` | Problema | Mínimo de cortes para transformar retângulo $a \times b$ em quadrados (CSES *Rectangle Cutting*). | Bottom-up 2D | $O(a b (a + b))$ |
| `DP/CountingNumber.cpp` | Template / Problema | **Digit DP**: inteiros em $[a, b]$ sem dois dígitos adjacentes iguais (CSES *Counting Numbers*). | Top-down 4D | $O(D \cdot 10 \cdot 4)$ |
| `DP/SumofDigits.cpp` | Template / Problema | **Digit DP**: soma dos dígitos de todos os inteiros em $[a, b]$ (SPOJ *CPCRC1C*). | Top-down 3D | $O(D \cdot 9D \cdot 2)$ |

---

## Detalhes e Armadilhas (*Gotchas*)

- **`CountingNumber.cpp`:** quando $a = 0$, `to_string(a - 1)` gera `"-1"`, o que quebra o loop de dígitos (`'-' - '0'` negativo). Trate $a = 0$ separadamente (como já é feito em `SumofDigits.cpp`: `a == 0 ? 0 : solve(a - 1)`). Além disso, na linha 23 grava em `dp[n][x][zeros][tight]` mesmo quando `x == -1` (acesso fora dos limites do array `dp[n][-1]`).
- **`SumofDigits.cpp`:** tabela `dp[10][90][2]` e assinatura `solve(int x)` limitam a entrada a $x < 10^9$. Para $10^{18}$, aumente para `dp[20][180][2]` e troque `int x` por `ll x`.
- **`IncreasingSubsequence.cpp`:** usa `lower_bound` (subsequência **estritamente** crescente). Para **não-decrescente**, basta trocar `lower_bound` por `upper_bound`.
- **`LCS.cpp`:** a reconstrução `r(i, j)` retorna `s[i] + r(i+1, j+1)` concatenando strings por valor (custo $O(L^2)$ em vez de $O(L)$); para strings até 3000 passa, mas um `while` iterativo com `push_back` é mais seguro contra TLE/MLE.
- **Estilo:** 9 dos 11 arquivos são snippets `void solve()` sem `main()`; apenas `LCS.cpp`, `rectangularcutting.cpp` e `SumofDigits.cpp` possuem `int main()`.

---

## Páginas Relacionadas

- [[wiki/padroes/dp-classicos-e-digit-dp|DP Clássicos e Digit DP]]
- [[wiki/padroes/busca-binaria-e-meet-in-the-middle|Busca Binária e Meet in the Middle]] (LIS com `lower_bound`)
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
