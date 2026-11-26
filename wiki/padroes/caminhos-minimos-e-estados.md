---
titulo: Caminhos Mínimos e Grafos com Estados
tipo: padrao
tags: [grafos, bfs, dijkstra, floyd-warshall, estados, arvore]
fontes:
  - raw/Competitive-Programming-Lib/Library/Grafos/BFS.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/BFSGRid.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijkstra.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijestados.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/dijestados2.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/floyd.cpp
  - raw/Competitive-Programming-Lib/Library/Grafos/MaxNodeDistance.cpp
atualizado: 2026-11-25
---

# Caminhos Mínimos e Grafos com Estados

Síntese dos algoritmos de distâncias e caminhos mínimos presentes em [[wiki/categorias/grafos|Grafos]], destacando como a lib evolui do BFS simples até o **Dijkstra em grafo de estados**.

---

## Comparação dos Algoritmos na Lib

| Tipo de Grafo / Pergunta | Algoritmo | Arquivo na Lib | Complexidade |
|---|---|---|---|
| Não-ponderado, fonte única ou destino único (grafo reverso) | BFS | `Grafos/BFS.cpp` | $O(V + E)$ |
| Não-ponderado em grid 2D com reconstrução de rota | BFS + tabela `parent` | `Grafos/BFSGRid.cpp` | $O(NM)$* |
| Ponderado ($w \ge 0$), fonte única | Dijkstra | `Grafos/dijkstra.cpp` | $O((V+E)\log V)$ |
| Ponderado ($w \ge 0$) com restrição extra ($k$ estados por vértice) | Dijkstra de Estados | `Grafos/dijestados.cpp`, `Grafos/dijestados2.cpp` | $O(k(V+E)\log(kV))$ |
| Ponderado (pode ter $w < 0$, sem ciclo negativo), todos os pares ($V \le 500$) | Floyd-Warshall | `Grafos/floyd.cpp` | $O(V^3)$ |
| Árvore: distância máxima a partir de cada nó | 3× BFS (Diâmetro) | `Grafos/MaxNodeDistance.cpp` | $O(V)$ |

*\*Em `BFSGRid.cpp`, o uso de `map` em `parent` adiciona $\log(NM)$; para grids $1000 \times 1000$, prefira matriz estática.*

---

## O Padrão "Grafo de Estados" na Lib

Dois arquivos demonstram a mesma técnica poderosa: expandir cada vértice $u$ em pares $(u, \text{estado})$ e rodar Dijkstra normal sobre `dist[u][estado]`:

1. **Estado cíclico (`Grafos/dijestados.cpp`):**
   - Estado: `(u, r)` onde `r = passos % 3` ($\in \{0, 1, 2\}$).
   - Transição: de `(u, r)` para `(v, (r + 1) % 3)` com custo `curr + w`.
   - Caso especial: `if (u == n) continue;` impede continuar andando após atingir o destino `n`.
2. **Estado de recurso/cupom (`Grafos/dijestados2.cpp` — CSES *Flight Discount*):**
   - Estado: `(u, used)` onde `used` $\in \{0, 1\}$ indica se o desconto de $50\%$ já foi gasto.
   - Transições:
     - Sempre: `(u, used) -> (v, used)` com custo `+ w`.
     - Se `!used`: `(u, 0) -> (v, 1)` com custo `+ w / 2`.
   - **Nota:** no final, prefira `min(dist[n][0], dist[n][1])` em vez de apenas `dist[n][1]`.

---

## Truques Importantes Capturados na Lib

- **Grafo Reverso (`Grafos/BFS.cpp`):** quando queremos a distância de **todos os nós até um único destino $T$** em grafo direcionado, invertemos as arestas (`adjr[destino].push_back(origem)`) e rodamos um único BFS partindo de $T$.
- **Propriedade do Diâmetro em Árvores (`Grafos/MaxNodeDistance.cpp`):** para qualquer nó $u$ de uma árvore, o nó mais distante de $u$ é sempre uma das extremidades $(v_1, v_2)$ do diâmetro. Logo:
  1. BFS a partir de `1` $\rightarrow$ acha extremidade $v_1$.
  2. BFS a partir de $v_1$ $\rightarrow$ calcula `dist1[]` e acha outra extremidade $v_2$.
  3. BFS a partir de $v_2$ $\rightarrow$ calcula `dist2[]`.
  4. Resposta para cada $v$: `max(dist1[v], dist2[v])`.
- **Arestas paralelas no Floyd-Warshall (`Grafos/floyd.cpp`):** já trata corretamente com `dist[a][b] = min(dist[a][b], c);` e previne overflow verificando `if (dist[i][k] < INF && dist[k][j] < INF)`.

---

## Páginas Relacionadas

- [[wiki/categorias/grafos|Grafos]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]] (alerta de `freopen` em `BFS.cpp` e `INF = LLONG_MAX`)
