---
titulo: Relatório de Lint Inicial
tipo: auditoria
tags: [lint, auditoria, bugs, lacunas, qualidade]
fontes:
  - raw/Competitive-Programming-Lib/contents.txt
atualizado: 2026-11-25
---

# Relatório de Lint Inicial (`2026-11-25`)

Primeira passagem de **Lint** (operação de auditoria do padrão LLM Wiki) sobre os 64 arquivos de `raw/Competitive-Programming-Lib/`.

> Como `raw/` é imutável na arquitetura da wiki, nenhum arquivo bruto foi alterado aqui. Todos os achados ficam documentados para consulta e para guiar futuras correções diretamente no repositório original.

---

## 1. Bugs e Armadilhas Reais no Código Bruto (12 achados)

| # | Severidade | Arquivo | Problema Encontrado | Correção Sugerida |
|---|---|---|---|---|
| 1 | **Alta (Fórmula errada)** | `TeoriaDosNumeros/relations.cpp` | Identidade de Pascal escrita errada nos comentários: $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n}{k-2}$. | Corrigir para $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$. |
| 2 | **Alta (UB)** | `Others/prefixsum2.cpp` | `ll prefix[MAXN+1];` local em `main()` sem inicializar `prefix[0] = 0;` — lê lixo de memória. | Inicializar `ll prefix[MAXN+1] = {0};` ou usar `vector<ll>`. |
| 3 | **Alta (Hardcoded I/O)** | `Grafos/BFS.cpp` | Linha 90 tem `freopen("jumping.in", "r", stdin);` hardcoded. | Remover antes de usar em qualquer outro problema. |
| 4 | **Alta (Overflow)** | `Others/cows.cpp` | `int mid = (l+r)/2;` enquanto `l` e `r` são `ll` (estoura se diferença $> 10^9$). | Usar `ll mid = l + (r - l) / 2;`. |
| 5 | **Alta (Precisão)** | `Geometria/ConvexHull.cpp` | `double v = AB.cross(BC);` converte `ll` para `double`, perdendo precisão para coordenadas $> 2^{26}$. | Manter `ll v = AB.cross(BC);`. |
| 6 | **Alta (Colisão)** | `Strings/Hash.cpp`, `Hash2.cpp`, `Hash3.cpp` | Mapeia `'a' -> 0` (`s[i] - 'a'`), fazendo `"a"` e `"aa"` terem o mesmo hash `0`. Além disso, `pref[i-1] * K` não usa `mod_mul` ($\approx 10^{18}$). | Mapear `(s[i] - 'a' + 1)` e usar `mod_mul` no pré-cálculo. |
| 7 | **Alta (Edge case / OOB)** | `DP/CountingNumber.cpp` | Quebra quando `a == 0` (`to_string(-1)`) e escreve em `dp[n][-1][...]` quando `x == -1`. | Tratar `a == 0` e não gravar em `dp` quando `x == -1`. |
| 8 | **Média (Limite)** | `Buscas/BB.cpp` | `int r = 1e7;` é pequeno demais para $a_i$ grandes e compara usando `double`. | Usar `ll r = 1e18;` e checagem inteira `contador + m > 2LL * n * a[n/2]`. |
| 9 | **Média (Edge case)** | `Grafos/DFS.cpp` | Não verifica se `grid[0][0] == 's'` antes de iniciar o DFS. | Retornar `false` imediatamente se `grid[0][0] != 's'`. |
| 10 | **Média (Overflow)** | `TeoriaDosNumeros/fastexp.cpp` | `fexp(a, b, m)` não aplica `a %= m` antes do loop (overflow se $a \ge 3 \cdot 10^9$). | Adicionar `a %= m;` no início de `fexp`. |
| 11 | **Média (Limite)** | `DP/SumofDigits.cpp` | `dp[10][90][2]` e `solve(int x)` limitam a $x < 10^9$. | Ampliar para `dp[20][180][2]` e `ll x` para suportar $10^{18}$. |
| 12 | **Baixa (Cola com UB)** | `Others/structs.cpp` | `int n; ll a[n];` antes de `cin >> n;` (VLA não inicializado) e `cMax = valMax + 'a'` (deveria ser `+'A'`). | Mover declaração após leitura e corrigir `+'A'`. |

---

## 2. Dessincronia do `contents.txt` (Caderno PDF)

O `contents.txt` lista apenas **27 de 64 arquivos** (**37 arquivos ficam de fora do PDF**!):
- **`DP/` (0 de 11 no PDF):** pasta inteira ausente no `contents.txt`.
- **`Strings/` (0 de 6 no PDF):** pasta inteira ausente no `contents.txt`.
- **`Others/` (0 de 6 no PDF):** seção existe mas está vazia.
- **`Range/` (3 de 9 no PDF):** faltam `segLazy.cpp`, `segtreewithcompression.cpp`, `listremoval.cpp`, `Pqueries.cpp`, `Range Xor Queries`, `RangeUpdateQueries`.
- **`TeoriaDosNumeros/` (3 de 7 no PDF):** faltam `commondivisors.cpp`, `fastexp.cpp`, `matrixexp.cpp`, `relations.cpp`.
- **`Buscas/` (4 de 6 no PDF):** faltam `BB.cpp` e `MM.cpp`.

---

## 3. Higiene de Arquivos e Organização

1. **Arquivos sem extensão `.cpp`:**
   - `Library/Range/Range Xor Queries` (tem espaços e sem `.cpp`)
   - `Library/Range/RangeUpdateQueries` (sem `.cpp`)
2. **Realocações conceituais sugeridas** (já resolvidas transversalmente na wiki):
   - `Others/cows.cpp` $\rightarrow$ pertence a [[wiki/categorias/buscas|Buscas]] (Busca Binária na Resposta).
   - `Others/primo.cpp` $\rightarrow$ pertence a [[wiki/categorias/teoria-dos-numeros|Teoria dos Números]].
   - `Grafos/backtrack.dfs.cpp` $\rightarrow$ mesma família de `Buscas/Queens.cpp` (Backtracking).
3. **Inconsistência de estilo:** 22+ arquivos são snippets `void solve()` sem `int main()`, e `segtreewithcompression.cpp` é a única SegTree 0-based (ver [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]).

---

## 4. Lacunas Clássicas de Programação Competitiva (Roadmap Sugerido)

Se for expandir a lib durante a semana de uso da wiki, as lacunas de maior retorno são:
- **Grafos:** Kruskal (reaproveitando `DSU.cpp`), LCA / Binary Lifting, SCC (Kosaraju/Tarjan), Bellman-Ford, Dinic (Max Flow).
- **Strings:** KMP ($\pi$-function) e Z-function (alternativas determinísticas a `Hash*.cpp`).
- **Teoria dos Números:** Euclides Estendido (`extgcd`) e fatoração rápida com SPF.
- **DP:** Bitmask DP (ex.: TSP / matching — otimizando `backtrack.dfs.cpp`) e Tree DP.
- **Geometria:** Interseção de segmentos e Área de Polígono (*Shoelace*).

---

## 5. Saúde Interna da Wiki

- **Cobertura de `raw/`:** 64 / 64 arquivos catalogados (100%).
- **Páginas órfãs:** 0 (todas as 15 páginas em `wiki/` estão indexadas em `index.md` e interligadas por wikilinks).
