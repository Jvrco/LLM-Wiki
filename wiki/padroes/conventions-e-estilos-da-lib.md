---
titulo: Convenções e Estilos da Lib
tipo: padrao
tags: [convencoes, estilo, indexacao, boilerplate, cpp]
fontes:
  - raw/Competitive-Programming-Lib/contents.txt
  - raw/Competitive-Programming-Lib/Library/Others/structs.cpp
atualizado: 2026-11-25
---

# Convenções e Estilos da Lib

Ao compilar os 64 arquivos de `raw/Competitive-Programming-Lib/`, fica evidente que a biblioteca reúne códigos de **dois estilos distintos de autoria** (típico de um time de Maratona/ICPC). Conhecer essas diferenças evita erros silenciosos ao copiar e misturar templates durante um contest.

---

## 1. Os Dois Perfis de Código na Lib

| Característica | Estilo A (Arquivos executáveis completos) | Estilo B (Snippets `void solve()`) |
|---|---|---|
| **Macro de quebra de linha** | `#define endl '\n'` | `#define endll '\n'` (note que mesmo assim usa `endl` no código!) |
| **Ponto de entrada** | Possui `int main()` com `ios::sync_with_stdio(false); cin.tie(NULL);` | Apenas `void solve()` **sem `int main()`** (pensado para colar dentro de um template base) |
| **Indexação em SegTree** | **1-based** (`node=1`, `[1, n]`, filhos `2*node`, `2*node+1`) | **0-based** (`node=0`, `[0, n-1]`, filhos `2*node+1`, `2*node+2` em `segtreewithcompression.cpp`) |
| **Exemplos típicos** | `dijkstra.cpp`, `DSU.cpp`, `Fenwicktree.cpp`, `segtree.cpp`, `segLazy.cpp`, `prim.cpp`, `floyd.cpp` | `bs1.cpp`, `bs2.cpp`, `MeetInTheMiddle.cpp`, `ConvexHull.cpp`, `Hash*.cpp`, `Dp*.cpp`, `Toposort.cpp` |

> **Atenção no `bs2.cpp`:** `#define endll '\n';` tem ponto-e-vírgula no final da macro!

---

## 2. Constantes `INF` e Risco de Overflow

- Vários arquivos do Estilo A declaram `const ll INF = LLONG_MAX;` ($\approx 9.22 \times 10^{18}$).
- **Perigo:** qualquer operação `INF + w` causa **overflow assinado (Undefined Behavior)** e vira número negativo!
- Em `floyd.cpp`, o código se protege explicitamente com `if (dist[i][k] < INF && dist[k][j] < INF)`.
- **Regra recomendada ao adaptar qualquer código da lib:** prefira `const ll INF = 1e18;` (como já aparece em `structs.cpp`, `ConvexHull.cpp`, `Dp2.cpp`, `DpJump.cpp`), que permite somar até $4 \times 10^{18}$ sem overflow.

---

## 3. Boilerplate Residual (Variáveis Globais Mortas)

Vários arquivos foram criados colando um cabeçalho padrão e carregam vetores globais não utilizados:
- `bool visited[MAXV];` e `vector<pair<int, ll>> adj[MAXV];` aparecem sem uso em `segtree.cpp`, `segLazy.cpp`, `listremoval.cpp`, `Pqueries.cpp`, `Range Xor Queries`, `DSU.cpp`, `combinatoria.cpp`, `prefixsum.cpp`, `prefixsum2.cpp`, `backtrack.dfs.cpp`, `Bicoloridade.cpp`.
- `int dx[4]`, `int dy[4]` aparecem sem uso em `Hurricane.cpp`, `PointLocation.cpp`, `Triangulo.cpp`, `fastexp.cpp`, `CycleDetection.cpp`.
- **Impacto prático:** além de poluir a leitura no caderno impresso, alocar `vector<pair<int, ll>> adj[1000000]` (como em `DSU.cpp`, `MAXV = 1e6`) consome ~24 MB de memória estática à toa.

---

## 4. Caderno PDF (`contents.txt`)

O arquivo `raw/Competitive-Programming-Lib/contents.txt` controla o que entra no PDF gerado por `generate_pdf.py` / `notebook.tex`. Atualmente ele indexa apenas **27 dos 64 arquivos** (detalhes completos em [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]).

---

## Páginas Relacionadas

- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/categorias/outros|Outros]] (`structs.cpp`)
