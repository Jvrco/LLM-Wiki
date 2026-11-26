# Registro da Atividade — LLM Wiki de Programação Competitiva

> Atividade baseada no conceito de **LLM Wiki** (Andrej Karpathy, gist `llm-wiki.md`, abril de 2026): em vez de o modelo redescobrir conhecimento dos documentos brutos a cada pergunta, um agente compila e mantém uma base estruturada que acumula conhecimento entre sessões.

---

## 1. De onde veio o material bruto

- **Repositório:** [Jvrco/Competitive-Programming-Lib](https://github.com/Jvrco/Competitive-Programming-Lib)
- **Localização imutável na wiki:** `raw/Competitive-Programming-Lib/`
- **Inventário real na data da ingestão (2026-11-25):**
  - **64 arquivos** de código C++ (~89,7 KB) distribuídos em **8 pastas** dentro de `Library/`:
    - `Grafos` (15), `DP` (11), `Range` (9), `TeoriaDosNumeros` (7), `Buscas` (6), `Strings` (6), `Others` (6), `Geometria` (4).
  - **Infraestrutura de caderno:** `contents.txt`, `notebook.tex`, `contents.tex`, `generate_pdf.py`, `getContents.py`.
- **Características reais do material bruto (que motivam a wiki):**
  - Mistura **templates reutilizáveis** com **soluções completas de problemas** (CSES, Codeforces, SPOJ, AtCoder) sem separação explícita.
  - Apresenta **dois estilos de autoria** (provavelmente de integrantes diferentes do time de maratona), com convenções distintas de indexação (0-based vs. 1-based), macros (`endl` vs. `endll`) e estrutura (`main()` vs. apenas `solve()`).
  - O índice original (`contents.txt`) estava defasado, deixando **37 arquivos de fora** do PDF do caderno (incluindo as pastas inteiras de `DP/` e `Strings/`).

---

## 2. Que estrutura foi adotada

Adotamos fielmente a arquitetura de **3 camadas** proposta no gist de Karpathy, adaptada para Programação Competitiva e compatível com Obsidian:

```text
cp-llm-wiki/
├── AGENTS.md                        # Schema: regras, convenções e operações (ingest, query, lint)
├── index.md                         # Catálogo de conteúdo (1 linha por página) — entrada para queries
├── log.md                           # Histórico cronológico append-only das ações do agente
├── diario-de-uso.md                 # Este registro da atividade
├── raw/                             # Camada 1: fonte bruta IMUTÁVEL (git clone da lib)
│   └── Competitive-Programming-Lib/
└── wiki/                            # Camada 2: conhecimento compilado e mantido pelo agente
    ├── categorias/                  # 8 mapas de domínio (inventário 1:1 dos 64 arquivos)
    ├── padroes/                     # 6 sínteses transversais (guias de decisão, trade-offs, convenções)
    └── auditoria/                   # Relatório de lint (bugs, riscos, lacunas e dessincronias)
```

### Por que essa estrutura (e não apenas "organizar pastas")?
1. **Conhecimento transversal:** na pasta bruta, `cows.cpp` está em `Others/`, `IncreasingSubsequence.cpp` em `DP/` e `bs1.cpp` em `Buscas/`. Na wiki, [[wiki/padroes/busca-binaria-e-meet-in-the-middle|Busca Binária e Meet in the Middle]] conecta todos eles num único mapa mental.
2. **Separação entre fonte bruta e conhecimento compilado:** `raw/` nunca é tocado pelo agente; bugs encontrados no código (como a identidade de Pascal errada em `relations.cpp` ou `prefix[0]` não inicializado em `prefixsum2.cpp`) ficam registrados em [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]] e nas páginas de categoria, evitando que o mesmo erro seja copiado de novo num contest.
3. **Ciclo de manutenção pelo agente (`ingest` / `query` / `lint`):** novas soluções ou notas de treino entram via `ingest`; dúvidas resolvidas que geram insights novos voltam para a wiki (*write-back*) via `query`; e o `lint` verifica drift e lacunas.

---

## 3. Como usar com o agente durante a semana (Comandos de Exemplo)

Para testar o padrão de verdade (deixando o agente **construir e manter**, não apenas consultar), use prompts como:

- **Query (com write-back):**
  > "Consultando `cp-llm-wiki/index.md`, qual estrutura da minha lib resolve range add + range sum? Se minha `segLazy.cpp` só faz range min, documente a adaptação necessária numa nota em `wiki/padroes/` e atualize o `log.md`."
- **Ingest (novo código ou editorial):**
  > "Adicionei o arquivo `KMP.cpp` (ou uma nota de contest) em `raw/`. Execute um `ingest` seguindo `cp-llm-wiki/AGENTS.md`."
- **Lint (manutenção):**
  > "Rode um `lint` em `cp-llm-wiki/` verificando se alguma página ficou órfã ou desatualizada em relação ao `raw/`."

---

## 4. Diário de 1 Semana de Uso (Preencher ao longo dos 7 dias)

> **Instrução da atividade:** registrar sobretudo **o que mudou no seu jeito de trabalhar após uma semana de uso**. Se não mudou nada, esse também é um achado honesto.

| Dia | Data | Operação feita (`ingest` / `query` / `lint`) | O que aconteceu na prática (ganho ou fricção)? |
|---|---|---|---|
| Dia 1 | 2026-11-25 | `ingest` inicial + `lint` inicial + 2 `query` (*write-back*) | Base compilada (64 arquivos -> 17 páginas). Lint revelou 12 bugs/armadilhas reais e 37 arquivos fora do `contents.txt`. |
| Simulação (Ciclo completo) | 2026-11-26 | `query` (mapa de problemas) + `ingest` (nota textual) + `lint` final | Wiki expandida para 19 páginas (0 órfãs, 0 links quebrados). Demonstração do acúmulo entre sessões com código + notas textuais em `raw/notas/`. |
| Dia 2 | | | *(preencher durante o uso real)* |
| Dia 3 | | | |
| Dia 4 | | | |
| Dia 5 | | | |
| Dia 6 | | | |
| Dia 7 | | | |

### Perguntas-guia para a síntese final (após 7 dias)
- [ ] **Reuso vs. recomeçar do zero:** Consultei a wiki antes de codar/debugar ou continuei indo direto nos `.cpp` / perguntando do zero ao LLM?
- [ ] **Acúmulo real:** Alguma resposta de `query` ou novo `ingest` realmente melhorou uma sessão posterior?
- [ ] **Custo de manutenção:** O agente manteve a wiki coerente sem dar mais trabalho do que economizou?
- [ ] **Veredito honesto:** O que efetivamente mudou (ou não mudou) no meu jeito de estudar/treinar Programação Competitiva?

> **Conclusão após 1 semana:** *(preencher no Dia 7)*
