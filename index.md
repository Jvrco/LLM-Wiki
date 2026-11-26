# Índice da LLM Wiki — Competitive Programming Lib

> Catálogo orientado a conteúdo. Antes de consultar arquivos em `raw/`, leia este índice para localizar diretamente as páginas compiladas relevantes.
> **Fonte bruta:** `raw/Competitive-Programming-Lib/` (`https://github.com/Jvrco/Competitive-Programming-Lib`) — 64 arquivos em 8 categorias.

---

## Mapas de Categorias (`wiki/categorias/`)

| Página | Arquivos | Resumo |
|---|---|---|
| [[wiki/categorias/buscas\|Buscas]] | 6 | Busca binária (2 templates + 1 problema), Meet in the Middle (soma exata e soma máxima mod $m$) e Backtracking (8 Rainhas). |
| [[wiki/categorias/dp\|Programação Dinâmica (DP)]] | 11 | Coin Change, Removing Digits, Grid Paths, Frog Jump, LIS $O(n \log n)$, Knapsack 0/1 e ilimitado, LCS com reconstrução, Rectangle Cutting e Digit DP (2 problemas). |
| [[wiki/categorias/geometria\|Geometria Computacional]] | 4 | Convex Hull (Monotone Chain / Andrew), orientação por produto vetorial, distância ponto-reta e contagem de triângulos retângulos em $y \in \{0, 1\}$. |
| [[wiki/categorias/grafos\|Grafos]] | 15 | BFS, BFS em grid com reconstrução, DFS iterativa/recursiva, Bicoloridade (2 versões), Detecção de Ciclo, Dijkstra padrão e com estados (2 versões), DSU, Floyd-Warshall, Diâmetro/Distância máxima em árvore, Prim (MST), Toposort (Kahn) e Backtracking. |
| [[wiki/categorias/range-queries\|Range Queries]] | 9 | Prefix Sum 2D, Fenwick Tree (soma e *difference array*), Segment Tree (mínimo, XOR, Lazy Propagation, Compressão de Coordenadas, $k$-ésimo elemento e Pizzeria Queries). |
| [[wiki/categorias/strings\|Strings]] | 6 | Rolling Hash polinomial (busca de padrão, bordas e períodos) e Trie (prefixos, palavra mais frequente por prefixo e Binary Trie para XOR mínimo). |
| [[wiki/categorias/teoria-dos-numeros\|Teoria dos Números]] | 7 | Combinatória iterativa e com inverso modular, Maior MDC de pares (Common Divisors), Crivo de Eratóstenes, Exponenciação Rápida (Fermat $a^{b^c}$), Exponenciação de Matrizes (Fibonacci) e cola de identidades. |
| [[wiki/categorias/outros\|Outros]] | 6 | Problemas e utilitários mistos: Aggressive Cows (busca binária), Prefix Sum (2 problemas), matriz prima (`primo.cpp`), Suffix Sum e cola de snippets C++ (`structs.cpp`). |

---

## Sínteses e Padrões Transversais (`wiki/padroes/`)

| Página | Resumo |
|---|---|
| [[wiki/padroes/guia-de-decisao-range-queries\|Guia de Decisão: Range Queries]] | Matriz comparativa para escolher entre Prefix Sum, Fenwick, SegTree, Lazy SegTree, Compressão de Coordenadas e variantes especializadas da lib. |
| [[wiki/padroes/adaptacoes-segtree-e-lazy\|Adaptações de Segment Tree e Lazy Propagation]] | *(query write-back)* Passo a passo para adaptar `segLazy.cpp` para Range Sum e Range Assign, e cuidados ao misturar 0-based e 1-based. |
| [[wiki/padroes/caminhos-minimos-e-estados\|Caminhos Mínimos e Grafos com Estados]] | Conecta BFS, BFS em grafo reverso, Grid BFS, Dijkstra clássico, Dijkstra com estado (resto mod 3 e cupom de desconto), Floyd-Warshall e distâncias em árvores. |
| [[wiki/padroes/busca-binaria-e-meet-in-the-middle\|Busca Binária e Meet in the Middle]] | Unifica os padrões de busca espalhados por `Buscas/`, `Others/` (`cows.cpp`, `prefixsum.cpp`) e `DP/` (`IncreasingSubsequence.cpp`). |
| [[wiki/padroes/dp-classicos-e-digit-dp\|DP Clássicos e Digit DP]] | Taxonomia das 11 implementações de DP (bottom-up vs. top-down, reconstrução de caminho, otimização por agrupamento de pesos e template de Digit DP). |
| [[wiki/padroes/hashing-e-trie\|Hashing Polinomial e Tries]] | Compara Rolling Hash vs. Trie na lib, documenta o uso de `__int128` e alerta sobre armadilhas de colisão (`'a' -> 0`) e overflow. |
| [[wiki/padroes/conventions-e-estilos-da-lib\|Convenções e Estilos da Lib]] | Mapeia os dois estilos de autoria presentes no repositório, convenções de indexação (0-based vs. 1-based), constantes `INF`/`MOD` e código boilerplate residual. |

---

## Auditoria e Saúde (`wiki/auditoria/`)

| Página | Resumo |
|---|---|
| [[wiki/auditoria/lint-inicial\|Relatório de Lint Inicial]] | Auditoria completa da lib: 12 bugs/armadilhas encontrados no código, dessincronia do `contents.txt` (37 arquivos fora do PDF), arquivos sem `.cpp`, realocações sugeridas e lacunas clássicas de CP. |
| [[wiki/auditoria/checklist-pre-contest\|Checklist Pré-Contest (Caderno PDF e Correções)]] | *(query write-back)* Lista priorizada de correções críticas e sincronização do `contents.txt` antes de gerar o PDF do caderno. |

---

## Registro da Atividade

- `RELATORIO.md` — Relatório consolidado da atividade (material bruto, estrutura adotada, evidências das operações e reflexões).
- `diario-de-uso.md` — Documentação da atividade e diário de acompanhamento para 1 semana de uso.
- `log.md` — Histórico cronológico de operações (`ingest`, `query`, `lint`).
