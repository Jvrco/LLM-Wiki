---
titulo: Mapa Reverso de Problemas Clássicos na Lib
tipo: padrao
tags: [problemas, cses, codeforces, atcoder, spoj, indice-reverso, query-writeback]
fontes:
  - wiki/categorias/buscas.md
  - wiki/categorias/dp.md
  - wiki/categorias/geometria.md
  - wiki/categorias/grafos.md
  - wiki/categorias/range-queries.md
  - wiki/categorias/strings.md
  - wiki/categorias/teoria-dos-numeros.md
  - wiki/categorias/outros.md
atualizado: 2026-11-26
---

# Mapa Reverso de Problemas Clássicos na Lib

> Página gerada por **`query` com *write-back***: mapeia diretamente problemas clássicos identificáveis em `raw/Competitive-Programming-Lib/` para o arquivo correspondente e a técnica associada na wiki.

---

## CSES Problem Set

| Problema | Arquivo na Lib | Técnica / Página na Wiki |
|---|---|---|
| *Meet in the Middle* | `Buscas/MeetInTheMiddle.cpp` | [[wiki/padroes/busca-binaria-e-meet-in-the-middle\|Meet in the Middle]] |
| *Chessboard and Queens* | `Buscas/Queens.cpp` | [[wiki/categorias/buscas\|Backtracking]] |
| *Minimizing Coins* | `DP/Dp1.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|Coin Change DP]] |
| *Removing Digits* | `DP/Dp2.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|DP Linear 1D]] |
| *Grid Paths* | `DP/DpGridPaths.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|Grid DP]] |
| *Increasing Subsequence* | `DP/IncreasingSubsequence.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|LIS O(n log n)]] |
| *Rectangle Cutting* | `DP/rectangularcutting.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|DP 2D]] |
| *Counting Numbers* | `DP/CountingNumber.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|Digit DP]] |
| *Point Location Test* | `Geometria/PointLocation.cpp` | [[wiki/categorias/geometria\|Produto Vetorial]] |
| *Labyrinth* | `Grafos/BFSGRid.cpp` | [[wiki/padroes/caminhos-minimos-e-estados\|BFS em Grid]] |
| *Round Trip* | `Grafos/CycleDetection.cpp` | [[wiki/categorias/grafos\|Detecção de Ciclo]] |
| *Shortest Routes I* | `Grafos/dijkstra.cpp` | [[wiki/padroes/caminhos-minimos-e-estados\|Dijkstra]] |
| *Flight Discount* | `Grafos/dijestados2.cpp` | [[wiki/padroes/caminhos-minimos-e-estados\|Dijkstra com Estados]] |
| *Shortest Routes II* | `Grafos/floyd.cpp` | [[wiki/padroes/caminhos-minimos-e-estados\|Floyd-Warshall]] |
| *Road Reparation* | `Grafos/prim.cpp` | [[wiki/categorias/grafos\|MST (Prim)]] |
| *Course Schedule* | `Grafos/Toposort.cpp` | [[wiki/categorias/grafos\|Toposort (Kahn)]] |
| *Tree Distances I* | `Grafos/MaxNodeDistance.cpp` | [[wiki/padroes/caminhos-minimos-e-estados\|Diâmetro em Árvore]] |
| *Forest Queries* | `Range/PrefixSum2d.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|Prefix Sum 2D]] |
| *Dynamic Range Sum Queries* | `Range/Fenwicktree.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|Fenwick Tree]] |
| *Range Update Queries* | `Range/RangeUpdateQueries` | [[wiki/padroes/guia-de-decisao-range-queries\|Fenwick + Diff Array]] |
| *Dynamic Range Minimum Queries* | `Range/segtree.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|Segment Tree]] |
| *Range Xor Queries* | `Range/Range Xor Queries` | [[wiki/padroes/guia-de-decisao-range-queries\|SegTree XOR]] |
| *List Removals* | `Range/listremoval.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|SegTree Order Statistic]] |
| *Pizzeria Queries* | `Range/Pqueries.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|Dual SegTree]] |
| *Salary Queries* | `Range/segtreewithcompression.cpp` | [[wiki/padroes/guia-de-decisao-range-queries\|SegTree + Compressão]] |
| *String Matching* | `Strings/Hash.cpp` | [[wiki/padroes/hashing-e-trie\|Rolling Hash]] |
| *Finding Borders* | `Strings/Hash2.cpp` | [[wiki/padroes/hashing-e-trie\|Rolling Hash]] |
| *Finding Periods* | `Strings/Hash3.cpp` | [[wiki/padroes/hashing-e-trie\|Rolling Hash]] |
| *Exponentiation II* | `TeoriaDosNumeros/fastexp.cpp` | [[wiki/categorias/teoria-dos-numeros\|Fermat + FastExp]] |
| *Distributing Apples* | `TeoriaDosNumeros/inversomodular.cpp` | [[wiki/categorias/teoria-dos-numeros\|Inverso Modular]] |
| *Common Divisors* | `TeoriaDosNumeros/commondivisors.cpp` | [[wiki/categorias/teoria-dos-numeros\|Série Harmônica / MDC]] |
| *Fibonacci Numbers* | `TeoriaDosNumeros/matrixexp.cpp` | [[wiki/categorias/teoria-dos-numeros\|Matrix Exp]] |

---

## Codeforces, AtCoder, SPOJ e Library Checker

| Plataforma / Problema | Arquivo na Lib | Técnica / Página na Wiki |
|---|---|---|
| Codeforces — *Robin Hood in Town* | `Buscas/BB.cpp` | [[wiki/padroes/busca-binaria-e-meet-in-the-middle\|Busca Binária na Resposta]] |
| Codeforces 888E — *Maximum Subsequence* | `Buscas/MM.cpp` | [[wiki/padroes/busca-binaria-e-meet-in-the-middle\|Meet in the Middle mod m]] |
| Codeforces — *Satyam and Counting* | `Geometria/Triangulo.cpp` | [[wiki/categorias/geometria\|Geometria / Hash Set]] |
| Codeforces 27D — *Ring Road 2* | `Grafos/Bicoloridade.cpp` | [[wiki/categorias/grafos\|Bipartição (BFS)]] |
| Codeforces 131C — *The World is a Theatre* | `TeoriaDosNumeros/combinatoria.cpp` | [[wiki/categorias/teoria-dos-numeros\|Combinatória]] |
| Codeforces 1926C — *Vlad and a Sum of Sum of Digits* | `Others/prefixsum2.cpp` | [[wiki/categorias/outros\|Prefix Sum]] |
| Codeforces 1436B — *Prime Square* | `Others/primo.cpp` | [[wiki/categorias/outros\|Primalidade]] |
| AtCoder — *Frog 2* | `DP/DpJump.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|DP Jump]] |
| AtCoder — *Knapsack 1* | `DP/Knapsack.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|Knapsack 0/1]] |
| AtCoder — *LCS* | `DP/LCS.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|LCS com Reconstrução]] |
| AtCoder ABC308 D — *Snuke Maze* | `Grafos/DFS.cpp` | [[wiki/categorias/grafos\|DFS em Grid]] |
| SPOJ — *AGGRCOW* | `Others/cows.cpp` | [[wiki/padroes/busca-binaria-e-meet-in-the-middle\|Busca Binária (Maximização)]] |
| SPOJ — *BUGLIFE* | `Grafos/DFS2.cpp` | [[wiki/categorias/grafos\|Bipartição (DFS)]] |
| SPOJ — *CPCRC1C* | `DP/SumofDigits.cpp` | [[wiki/padroes/dp-classicos-e-digit-dp\|Digit DP]] |
| Library Checker — *Set Xor-Min* | `Strings/TrieXorMin.cpp` | [[wiki/padroes/hashing-e-trie\|Binary Trie]] |

---

## Páginas Relacionadas

- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/padroes/guia-de-decisao-range-queries|Guia de Decisão: Range Queries]]
- [[wiki/padroes/caminhos-minimos-e-estados|Caminhos Mínimos e Grafos com Estados]]
