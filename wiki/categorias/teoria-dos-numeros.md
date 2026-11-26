---
titulo: Teoria dos Números
tipo: categoria
tags: [teoria-dos-numeros, combinatoria, crivo, exponenciacao-rapida, inverso-modular, matriz]
fontes:
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/combinatoria.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/commondivisors.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/crivo.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/fastexp.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/inversomodular.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/matrixexp.cpp
  - raw/Competitive-Programming-Lib/Library/TeoriaDosNumeros/relations.cpp
atualizado: 2026-11-25
---

# Teoria dos Números

Mapa compilado da pasta `Library/TeoriaDosNumeros/` (7 arquivos). Apenas 3 (`combinatoria.cpp`, `crivo.cpp`, `inversomodular.cpp`) estão no `contents.txt`.

> **Conexão fora desta pasta:** veja também `Others/primo.cpp` (teste de primalidade $O(\sqrt{x})$).

---

## Inventário

| Arquivo | Tipo | Algoritmo / Problema | Complexidade | No `contents.txt`? |
|---|---|---|---|---|
| `TeoriaDosNumeros/crivo.cpp` | Template | **Crivo de Eratóstenes** retornando `vector<bool> ehPrimo(n+1)`. | $O(n \log \log n)$ | Sim |
| `TeoriaDosNumeros/fastexp.cpp` | Template | **Exponenciação rápida modular** `fexp(a, b, m)` + redução de string mod $m$ + torre $a^{b^c} \bmod (10^9+7)$ via Pequeno Teorema de Fermat (CSES *Exponentiation II*). | $O(\log b)$ | **Não** |
| `TeoriaDosNumeros/inversomodular.cpp` | Template / Problema | **Fatorial + Inverso Modular em $O(N)$** (`fact[]` e `invfact[]` com um único `modxp(fact[N], MOD-2, MOD)`) + aplicação de *Stars and Bars* $\binom{n+m-1}{m}$ (CSES *Distributing Apples*). | $O(N + \log \text{MOD})$ | Sim |
| `TeoriaDosNumeros/combinatoria.cpp` | Problema | **Coeficiente binomial sem módulo** `comb(n, k)` iterativo multiplicando e dividindo a cada passo + exemplo de contagem de times (Codeforces 131C *The World is a Theatre*). | $O(k)$ | Sim |
| `TeoriaDosNumeros/commondivisors.cpp` | Problema | **Maior MDC entre quaisquer dois elementos** do array via contagem de múltiplos na série harmônica (CSES *Common Divisors*). | $O(M \log M)$ | **Não** |
| `TeoriaDosNumeros/matrixexp.cpp` | Template | **Exponenciação de matrizes $2 \times 2$** para calcular $F_n \bmod (10^9+7)$ (CSES *Fibonacci Numbers*). | $O(m^3 \log n)$ | **Não** |
| `TeoriaDosNumeros/relations.cpp` | Cola / Notas | Resumo em comentários de Fermat, inverso modular e identidades binomiais. | — | **Não** |

---

## Detalhes e Armadilhas (*Gotchas*)

- **BUG na cola `relations.cpp` (linhas 272–273):**
  A identidade de Pascal está anotada como $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n}{k-2}$, o que está **incorreto**! A fórmula correta é:
  $$\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$$
- **`fastexp.cpp` — Base sem módulo inicial:** `fexp(a, b, m)` não faz `a %= m` antes do `while`. Se `a` vier grande ($\ge 3 \times 10^9$), `a * a` dará overflow em `ll` na primeira iteração. (Compare com `inversomodular.cpp`, que faz `base = base % mod;` corretamente!)
- **`crivo.cpp`:** inclui prompts interativos (`std::cout << "Digite o valor de n: ";`) no `main()`; ao usar em contest, copie apenas a função `crivoEratostenes(int n)`.
- **`combinatoria.cpp`:** `comb(n, k)` faz `ans *= (n - i); ans /= (i + 1);` sem módulo — seguro até $n \le 60$ em `ll`, mas para $n$ maior dê preferência a `inversomodular.cpp` (com módulo primo).
- **`commondivisors.cpp`, `fastexp.cpp`, `matrixexp.cpp`:** snippets `void solve()` sem `int main()`.

---

## Lacunas nesta Categoria

Ausentes na lib atual: **Euclides Estendido** (`extgcd` para inverso modular quando $m$ não é primo), **Fatoração com SPF** (*Smallest Prime Factor* via crivo linear/modificado) e **Função Totiente de Euler** ($\phi(n)$).

---

## Páginas Relacionadas

- [[wiki/categorias/outros|Outros]] (`primo.cpp` — primalidade $O(\sqrt{x})$)
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
