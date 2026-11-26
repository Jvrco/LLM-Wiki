# Relatório da Atividade — LLM Wiki de Programação Competitiva

**Conceito de referência:** *LLM Wiki* (Andrej Karpathy, gist `llm-wiki.md`, abril de 2026) — em vez de o modelo redescobrir conhecimento dos documentos brutos a cada pergunta, um agente compila e mantém uma base estruturada em Markdown, fazendo o conhecimento se acumular entre sessões.

---

## 1. De onde veio o material bruto

O material bruto veio diretamente da minha biblioteca pessoal/de time de programação competitiva no GitHub:

- **Repositório:** [https://github.com/Jvrco/Competitive-Programming-Lib](https://github.com/Jvrco/Competitive-Programming-Lib) (snapshot capturado no commit `49ccee9` em `raw/Competitive-Programming-Lib/`).
- **Volume:** **64 arquivos de código C++** (~89,7 KB) distribuídos em **8 pastas** dentro de `Library/`, além dos arquivos de geração do caderno impresso em LaTeX (`contents.txt`, `notebook.tex`, `contents.tex`, `generate_pdf.py`, `getContents.py`).

| Categoria (`Library/`) | Qtde. de arquivos | Exemplos de conteúdo |
|---|---:|---|
| `Grafos` | 15 | BFS, BFS em grid, DFS, Bicoloridade, Detecção de Ciclo, Dijkstra (padrão e com estados), DSU, Floyd-Warshall, Prim, Toposort, Diâmetro de árvore |
| `DP` | 11 | Coin Change, Grid Paths, Frog Jump, LIS $O(n \log n)$, Knapsack 0/1 e ilimitado, LCS com reconstrução, Rectangle Cutting, Digit DP |
| `Range` | 9 | Prefix Sum 2D, Fenwick Tree (soma e *difference array*), SegTree (min, XOR, Lazy, Compressão de Coordenadas, $k$-ésimo elemento, Pizzeria Queries) |
| `TeoriaDosNumeros` | 7 | Crivo, Exponenciação Rápida, Inverso Modular, Combinatória, Common Divisors, Exponenciação de Matrizes, cola de relações |
| `Buscas` | 6 | Busca Binária (invariante e na resposta), Meet in the Middle (soma exata e mod $m$), 8 Rainhas |
| `Strings` | 6 | Rolling Hash (matching, bordas, períodos), Trie de prefixos, Trie de frequência, Binary Trie (XOR mínimo) |
| `Others` | 6 | Aggressive Cows, Prefix/Suffix Sum, primalidade, cola de snippets (`structs.cpp`) |
| `Geometria` | 4 | Convex Hull (Monotone Chain), orientação por produto vetorial, distância ponto-reta, triângulos retângulos |
| **Total** | **64** | **100% ingeridos na wiki** |

### Diagnóstico do estado bruto (por que uma pasta de `.cpp` não basta)
Ao analisar o repositório bruto, ficaram evidentes três problemas típicos de materiais reais acumulados ao longo de treinos:
1. **Mistura sem distinção** entre *templates reutilizáveis* e *soluções pontuais de problemas* (CSES, Codeforces, SPOJ, AtCoder).
2. **Dois estilos de autoria convivendo** sem documentação: um estilo com `int main()`, `#define endl '\n'` e SegTree 1-based, e outro estilo com snippets `void solve()` sem `main()`, `#define endll '\n'` e SegTree 0-based (`segtreewithcompression.cpp`).
3. **Defasagem documental:** o `contents.txt` (usado para gerar o PDF do caderno) incluía apenas **27 dos 64 arquivos**, deixando de fora 100% das pastas `DP/` e `Strings/`.

---

## 2. Que estrutura foi adotada

Adotei fielmente a arquitetura de **3 camadas** do padrão LLM Wiki de Karpathy, compatível com visualização em grafo no **Obsidian** (via wikilinks `[[...]]` e frontmatter YAML):

```text
cp-llm-wiki/
├── AGENTS.md                  # Camada de Schema: regras, convenções e operações do agente
├── index.md                   # Catálogo orientado a conteúdo (1 linha por página)
├── log.md                     # Histórico cronológico append-only (ingest / query / lint)
├── diario-de-uso.md           # Registro diário para acompanhamento de 1 semana
├── RELATORIO.md               # Este relatório
├── raw/                       # Camada 1 (IMUTÁVEL): cópia intacta da lib original
│   └── Competitive-Programming-Lib/
└── wiki/                      # Camada 2 (COMPILADA E MANTIDA PELO AGENTE):
    ├── categorias/            # 8 mapas de domínio (inventário 1:1 dos 64 arquivos)
    ├── padroes/               # 7 sínteses transversais (guias de decisão, trade-offs, adaptações)
    └── auditoria/             # 2 relatórios de saúde (lint inicial + checklist pré-contest)
```

### Como o agente constrói e mantém (não apenas consulta)
O arquivo [AGENTS.md](AGENTS.md) define três operações explícitas, todas já exercitadas na construção desta base (registradas em [log.md](log.md)):

1. **`ingest` (Compilação):** o agente leu todos os 64 arquivos de `raw/`, extraiu complexidade, indexação, problema de origem e *gotchas*, gerou os 8 mapas em `wiki/categorias/` e sintetizou 6 páginas transversais em `wiki/padroes/` — conectando, por exemplo, `Others/cows.cpp`, `DP/IncreasingSubsequence.cpp` e `Buscas/` numa única página de busca binária (`wiki/padroes/busca-binaria-e-meet-in-the-middle.md`).
2. **`lint` (Auditoria de saúde):** o agente varreu a base procurando bugs, contradições, arquivos órfãos e desalinhamentos, produzindo [wiki/auditoria/lint-inicial.md](wiki/auditoria/lint-inicial.md). Essa única passagem encontrou **12 bugs/armadilhas reais** que estavam escondidos na lib:
   - Identidade de Pascal escrita errada em `TeoriaDosNumeros/relations.cpp` ($\binom{n-1}{k-1}+\binom{n}{k-2}$ em vez de $\binom{n-1}{k-1}+\binom{n-1}{k}$);
   - `ll prefix[MAXN+1];` local sem zerar `prefix[0]` em `Others/prefixsum2.cpp` (Undefined Behavior);
   - `freopen("jumping.in", "r", stdin);` esquecido em `Grafos/BFS.cpp`;
   - `int mid = (l+r)/2;` dentro de busca `long long` em `Others/cows.cpp`;
   - `double v = AB.cross(BC);` perdendo precisão inteira em `Geometria/ConvexHull.cpp`;
   - Mapeamento `'a' -> 0` nos 3 arquivos `Strings/Hash*.cpp` (fazendo `"a"` e `"aa"` colidirem em hash `0`).
3. **`query` com *write-back* (Acúmulo entre sessões):** ao consultar *"como adaptar `segLazy.cpp` de range min para range sum/assign"* e *"o que corrigir antes de imprimir o caderno PDF"*, o agente consultou `index.md`, respondeu com base na wiki e **persistiu** as sínteses de volta como páginas permanentes:
   - [wiki/padroes/adaptacoes-segtree-e-lazy.md](wiki/padroes/adaptacoes-segtree-e-lazy.md)
   - [wiki/auditoria/checklist-pre-contest.md](wiki/auditoria/checklist-pre-contest.md)

---

## 3. O que mudou no jeito de trabalhar (e registro honesto da semana de uso)

### Mudanças já observadas na montagem e primeiras sessões (Dia 1 — 2026-11-25)
Mesmo antes de completar 7 dias, a mudança de paradigma em relação a simplesmente "ter uma pasta de `.cpp` no GitHub" ou "jogar arquivos num chat" já foi concreta:

1. **A lib deixou de ser um depósito passivo e virou um artefato auditado:** vários bugs latentes (`relations.cpp`, `BFS.cpp`, `Hash*.cpp`, `ConvexHull.cpp`) estavam na biblioteca há meses e só vieram à tona quando o agente precisou *compilar* cada arquivo em conhecimento estruturado e rodar o `lint`.
2. **Navegação por problema/decisão em vez de por nome de arquivo:** antes, lembrar onde estava uma técnica exigia saber o nome exato do `.cpp` (ex.: `Pqueries.cpp`, `MM.cpp`, `cows.cpp` em `Others/`). Agora, páginas como `guia-de-decisao-range-queries.md` e `index.md` respondem direto *"qual estrutura usar para este tipo de query?"*.
3. **Adaptações não evaporam:** explicar ao modelo como transformar `segLazy.cpp` (min) em soma, ou lembrar que `segtreewithcompression.cpp` é o único 0-based da pasta, antes exigia repetir o contexto em todo chat novo; agora fica registrado via *write-back* na própria wiki.

### Acompanhamento da semana de uso (Dias 2 a 7)
> **Nota de honestidade:** a wiki foi construída em **2026-11-25**. O acompanhamento diário dos 7 dias está estruturado em [diario-de-uso.md](diario-de-uso.md) para registrar, sem fabricar resultados, se o hábito de usar `ingest`/`query`/`lint` realmente se sustenta na rotina de treinos ou se, na prática, a fricção faz voltar ao fluxo antigo.

**Hipóteses que serão validadas ao fim da semana em `diario-de-uso.md`:**
- **Ganho esperado:** menos tempo perdido caçando templates e debugando erros recorrentes (indexação 0/1-based, `INF = LLONG_MAX`, bugs de hash).
- **Risco real (fricção):** se durante um treino rápido for mais veloz abrir o `.cpp` direto ou perguntar do zero ao LLM sem rodar `ingest`/`write-back`, a wiki pode ficar desatualizada — o que também será registrado honestamente como achado.
