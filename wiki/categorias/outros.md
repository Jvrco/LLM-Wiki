---
titulo: Outros
tipo: categoria
tags: [outros, prefix-sum, suffix-sum, busca-binaria, primalidade, snippets]
fontes:
  - raw/Competitive-Programming-Lib/Library/Others/cows.cpp
  - raw/Competitive-Programming-Lib/Library/Others/prefixsum.cpp
  - raw/Competitive-Programming-Lib/Library/Others/prefixsum2.cpp
  - raw/Competitive-Programming-Lib/Library/Others/primo.cpp
  - raw/Competitive-Programming-Lib/Library/Others/structs.cpp
  - raw/Competitive-Programming-Lib/Library/Others/suffixsum.cpp
atualizado: 2026-11-25
---

# Outros

Mapa compilado da pasta `Library/Others/` (6 arquivos). A seção `[Others]` existe no `contents.txt`, mas está **vazia** (nenhum dos 6 arquivos é exportado para o PDF).

Esta pasta concentra soluções avulsas que na verdade pertencem conceitualmente a outras categorias (`Buscas`, `Range`, `TeoriaDosNumeros`), além de um arquivo de cola de snippets C++ (`structs.cpp`).

---

## Inventário

| Arquivo | Tipo | Conteúdo / Problema | Categoria Conceitual | Complexidade |
|---|---|---|---|---|
| `Others/cows.cpp` | Problema | **Busca binária na resposta** maximizando a distância mínima entre $c$ vacas (SPOJ *AGGRCOW*). | [[wiki/categorias/buscas\|Buscas]] | $O(n \log n + n \log R)$ |
| `Others/prefixsum.cpp` | Problema | **Prefix Sum + `upper_bound` + agrupamento por frequência**: verifica se cada elemento consegue "comer" todos os demais (estilo *Slimes / Fish*, imprime `T`/`N`). | [[wiki/categorias/range-queries\|Range]] / [[wiki/categorias/buscas\|Buscas]] | $O(n \log n)$ |
| `Others/prefixsum2.cpp` | Problema | **Pré-cálculo com Prefix Sum** da soma de dígitos de $1 \dots n$ até `MAXN = 200000` (Codeforces 1926C *Vlad and a Sum of Sum of Digits*). | [[wiki/categorias/range-queries\|Range]] | $O(\text{MAXN} \log_{10} \text{MAXN} + q)$ |
| `Others/suffixsum.cpp` | Problema | **Suffix Sum** guloso: `ans = suffix[0] + sum(max(suffix[i], 0))` para particionar array maximizando soma ponderada. | [[wiki/categorias/range-queries\|Range]] | $O(n)$ |
| `Others/primo.cpp` | Problema | **Primalidade $O(\sqrt{x})$** (`prime(x)`) + construção de matriz $n \times n$ com `1` fora da diagonal e composto `x` na diagonal tal que `x + n - 1` é primo (Codeforces 1436B *Prime Square*). | [[wiki/categorias/teoria-dos-numeros\|Teoria dos Números]] | $O(n^2)$ |
| `Others/structs.cpp` | Cola / Snippets | Template base + macros (`fIo`, `pii`, `pll`, `tri`, `quad`), `newLogK`, comparação/XOR de strings binárias, `minHeap`, conversões `char <-> int` e `setprecision(6)`. | Utilitários C++ | — |

---

## Detalhes e Armadilhas (*Gotchas*)

- **BUG (Undefined Behavior) em `prefixsum2.cpp` (linha 186):**
  `ll prefix[MAXN+1];` é declarado localmente dentro de `main()` **sem inicializar `prefix[0] = 0;`**. O loop começa em `i = 1` lendo `prefix[0]`, que contém lixo de memória! Corrigir com `ll prefix[MAXN+1] = {0};` ou `vector<ll> prefix(MAXN+1, 0);`.
- **BUG de overflow em `cows.cpp` (linha 43):**
  `l` e `r` são `ll`, mas `int mid = (l+r)/2;` trunca para `int` de 32 bits! Se `arr[n-1] - arr[0] > 10^9`, ocorre overflow. Trocar por `ll mid = l + (r - l) / 2;`.
- **Bugs de cola em `structs.cpp`:**
  - Linha 287: `int n; ll a[n];` declara VLA com `n` não inicializado antes de `cin >> n;` (UB se executado).
  - Linha 297: `char cMax = valMax + 'a';` tem typo — deveria ser `valMax + 'A'` (para converter de volta para maiúscula).
  - Linha 264: `newLogK(n, k)` calcula $\log_k(n)$ usando `log(n) / log(k)` (base natural $e$, não base 10 como diz o comentário, embora o quociente dê o mesmo resultado $\log_k(n)$).

---

## Páginas Relacionadas

- [[wiki/padroes/busca-binaria-e-meet-in-the-middle|Busca Binária e Meet in the Middle]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
