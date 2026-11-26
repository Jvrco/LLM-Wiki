---
titulo: Grafos
tipo: categoria
tags: [grafos, bfs, dfs, dijkstra, dsu, floyd-warshall, prim, toposort, arvore]
fontes:
  - raw/Competitive-Programming-Lib/Library/Grafos/backtrack.dfs.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/BFS.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/BFSGRid.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/Bicoloridade.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/CycleDetection.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/DFS.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/DFS2.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijestados.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijestados2.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijkstra.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/DSU.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/floyd.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/MaxNodeDistance.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/prim.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/Toposort.cpp
atualizado: 2026-11-25
---

# Grafos

Mapa compilado da pasta `Library/Grafos/` (15 arquivos — a maior categoria da lib). Todos os 15 arquivos estão listados no `contents.txt`.

Síntese detalhada de caminhos mínimos e estados em [[wiki/padroes/caminhos-minimos-e-estados|Caminhos Mínimos e Grafos com Estados]].

---

## Inventário

| Arquivo | Tipo | Algoritmo / Problema | Complexidade | Indexação |
|---|---|---|---|---|
| `Grafos/BFS.cpp` | Problema | BFS em **grafo reverso** a partir do destino $n-1$ (problema *Jumping*). | $O(V + E)$ | 0-based |
| `Grafos/BFSGRid.cpp` | Template / Problema | BFS em grid 2D (`'A'` $\to$ `'B'`, obstáculos `'#'`) com **reconstrução do caminho** (`L/R/U/D`, CSES *Labyrinth*). | $O(NM \log(NM))$* | 0-based |
| `Grafos/DFS.cpp` | Problema | DFS iterativa (com `stack`) em grid seguindo ciclo `"snuke"` (AtCoder ABC308 D). | $O(HW)$ | 0-based |
| `Grafos/DFS2.cpp` | Template / Problema | **Bicoloridade / Bipartição via DFS** recursiva (SPOJ *BUGLIFE*). | $O(V + E)$ | 1-based |
| `Grafos/Bicoloridade.cpp` | Problema | **Bicoloridade / Bipartição via BFS** em grafo de interseção de cordas em círculo (Codeforces 27D *Ring Road 2*). | $O(m^2)$ | 0-based |
| `Grafos/CycleDetection.cpp` | Template | Detecção e reconstrução de **ciclo de tamanho $\ge 3$ em grafo não-direcionado** via DFS (CSES *Round Trip*). | $O(V + E)$ | 1-based |
| `Grafos/dijkstra.cpp` | Template | **Dijkstra padrão** com `priority_queue` min-heap em grafo direcionado (CSES *Shortest Routes I*). | $O((V + E) \log V)$ | 1-based |
| `Grafos/dijestados.cpp` | Problema | **Dijkstra com estados** $(u, r \bmod 3)$ em grafo não-direcionado (compara distâncias de chegada em $n$ com $0, 1, 2 \pmod 3$). | $O(3(V+E)\log V)$ | 1-based |
| `Grafos/dijestados2.cpp` | Template / Problema | **Dijkstra com estados** $(u, \text{used} \in \{0,1\})$: 1 cupom de desconto $w/2$ (CSES *Flight Discount*). | $O(2(V+E)\log V)$ | 1-based |
| `Grafos/floyd.cpp` | Template | **Floyd-Warshall** (*All-Pairs Shortest Path*) em grafo não-direcionado com tratamento de arestas múltiplas (CSES *Shortest Routes II*). | $O(V^3)$ | 1-based |
| `Grafos/DSU.cpp` | Template | **Union-Find (DSU)** com *Path Compression* e *Union by Size*; exemplo calcula produto dos tamanhos das componentes mod $10^9+7$. | $O(\alpha(n))$ | 1-based |
| `Grafos/prim.cpp` | Template | **Árvore Geradora Mínima (MST) — Algoritmo de Prim** com `priority_queue`; retorna `-1` (`IMPOSSIBLE`) se desconexo (CSES *Road Reparation*). | $O((V+E)\log V)$ | 1-based |
| `Grafos/Toposort.cpp` | Template | **Ordenação Topológica (Kahn / BFS)** com detecção de ciclo (`ans.size() < n`, CSES *Course Schedule*). | $O(V + E)$ | 1-based |
| `Grafos/MaxNodeDistance.cpp` | Template | **Distância máxima a partir de cada nó em árvore** via 3 BFS (achando extremidades $v_1, v_2$ do diâmetro, CSES *Tree Distances I*). | $O(V)$ | 1-based |
| `Grafos/backtrack.dfs.cpp` | Problema | Backtracking de permutação/matching em matriz $n \times n$ ($n \le 15$) maximizando soma `sk[idx][j]`. | $O(n!)$ | 0-based |

*\*`BFSGRid.cpp` usa `map<pair<int,int>, ...> parent`, adicionando fator $\log(NM)$; trocar por matriz 2D `parent[MAXV][MAXV]` reduz para $O(NM)$.*

---

## Detalhes e Armadilhas (*Gotchas*)

- **`BFS.cpp`:** contém `freopen("jumping.in", "r", stdin);` na linha 90! **Nunca copie sem remover essa linha** em juízes que usam `stdin`.
- **`DFS.cpp`:** não valida se `grid[0][0] == 's'` antes de empurrar `(0, 0)` na pilha — dá resposta errada se a célula inicial não for `'s'`.
- **`BFSGRid.cpp`:** `MAXV = 1000`, `visited[MAXV][MAXV]` e `map` para `parent` (pode ser lento para $1000 \times 1000$ se o limite de tempo for apertado).
- **`dijestados2.cpp`:** imprime apenas `dist[n][1]`. Se existir caminho ótimo sem usar desconto (ou $n = 1$), o ideal é `min(dist[n][0], dist[n][1])`.
- **`backtrack.dfs.cpp`:** está na pasta `Grafos/`, mas conceitualmente pertence à família de **Backtracking** (junto com `Buscas/Queens.cpp`). Para $n \le 20$, o mesmo problema pode ser otimizado para $O(n \cdot 2^n)$ com Bitmask DP.
- **`CycleDetection.cpp`, `MaxNodeDistance.cpp`, `Toposort.cpp`:** snippets `void solve()` sem `int main()`.

---

## Lacunas nesta Categoria

Ausentes na lib atual: **Kruskal** (já existe `DSU.cpp`, fácil de montar), **LCA / Binary Lifting**, **SCC (Kosaraju / Tarjan)**, **Bellman-Ford**, **Pontes / Pontos de Articulação** e **Fluxo Máximo (Dinic)**.

---

## Páginas Relacionadas

- [[wiki/padroes/caminhos-minimos-e-estados|Caminhos Mínimos e Grafos com Estados]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
