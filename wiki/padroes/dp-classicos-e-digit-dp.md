---
titulo: DP Clássicos e Digit DP
tipo: padrao
tags: [dp, knapsack, digit-dp, lis, lcs, bottom-up, top-down]
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

# DP Clássicos e Digit DP

Taxonomia das 11 implementações em [[wiki/categorias/dp|Programação Dinâmica (DP)]], organizadas por família de estado e transição.

---

## 1. DP Linear 1D e Mochila (Knapsack)

- **Coin Change / Unbounded Knapsack:**
  - `DP/Dp1.cpp`: `dp[i] = min(dp[i], 1 + dp[i - coin])` — minimiza quantidade de moedas.
  - `DP/Knapsack2.cpp`: truque valioso de **agrupamento por peso**! Como o peso é o tamanho de uma string (`sz = s.size()`), vários itens têm o mesmo peso; manter apenas `m[sz] = max(m[sz], v)` reduz o número de itens distintos para $O(\sqrt{\sum |s|})$, viabilizando $O(W \cdot D)$ mesmo com $n, W \le 2 \cdot 10^5$.
- **Knapsack 0/1 (`DP/Knapsack.cpp`):**
  - Top-down `memo[w][i]` ($O(n \cdot W)$ em tempo e memória). Se $n \cdot W$ apertar a memória, converta para bottom-up 1D iterando `w` **de trás para frente** (`for (int c = W; c >= peso; c--)`).
- **Transições sobre o próprio estado:**
  - `DP/Dp2.cpp` (*Removing Digits*): `dp[i] = min(dp[i - d] + 1)` para cada dígito $d$ de $i$.
  - `DP/DpJump.cpp` (*Frog 2*): `dp[i] = min_{1 <= j <= k} (|h[i] - h[i-j]| + dp[i-j])`.

---

## 2. DP em Grid, Strings e Intervalos

- **Grid (`DP/DpGridPaths.cpp`):** `dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % MOD` se `grid[i][j] != '*'`. Atenção à inicialização da linha 0 e coluna 0 (qualquer `'*'` bloqueia o resto da borda).
- **LCS com Reconstrução (`DP/LCS.cpp`):** calcula a tabela `dp[i][j]` top-down e depois reconstrói a subsequência seguindo o ramo que empata com `LCS(i, j)`.
- **Cortes 2D (`DP/rectangularcutting.cpp`):** `dp[i][j]` testa todos os cortes horizontais $k \in [1, i-1]$ e verticais $k \in [1, j-1]$, com base `dp[i][i] = 0`.
- **LIS $O(n \log n)$ (`DP/IncreasingSubsequence.cpp`):** mantém vetor `aux` onde `aux[len-1]` é o menor valor final possível de uma subsequência crescente de tamanho `len`.

---

## 3. Digit DP (Contagem e Soma em $[a, b]$)

A lib possui dois excelentes exemplares de **Digit DP** usando o padrão `F(b) - F(a - 1)`:

| Aspecto | `DP/CountingNumber.cpp` | `DP/SumofDigits.cpp` |
|---|---|---|
| **Objetivo** | Contar inteiros sem dígitos adjacentes iguais | Somar todos os dígitos dos inteiros em $[a, b]$ |
| **Estado** | `(n_restante, ultimo_digito, leading_zeros, tight)` | `(pos, soma_acumulada, tight)` |
| **Leading zeros importa?** | **Sim** (`0005` não deve proibir dois zeros à esquerda) | **Não** (somar `0` não altera a soma de dígitos) |
| **Caso base** | Retorna `1` (um número válido formado) | Retorna `sum` (a soma acumulada daquele número) |
| **Bug/Limite conhecido** | Quebra em $a = 0$ (`to_string(-1)`) e grava em `dp[n][-1]` | `dp[10][90][2]` + `int x` limita a $10^9$ |

### Checklist seguro para qualquer Digit DP
1. Sempre trate $a = 0$ explicitamente (`ansA = (a == 0 ? 0 : solve(a - 1))`).
2. Nunca indexe `dp` com `x == -1`; só leia/grave `dp` quando `!tight && !leading_zeros` (ou mapeie `x = 10` para "nenhum dígito ainda").
3. Para entradas até $10^{18}$, use `ll` e dimensões para 20 dígitos (`sum <= 180`).

---

## Páginas Relacionadas

- [[wiki/categorias/dp|Programação Dinâmica (DP)]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
