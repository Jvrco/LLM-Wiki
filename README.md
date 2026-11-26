# CP LLM Wiki — Base de Conhecimento Compilada por Agente

Implementação prática do padrão **LLM Wiki** proposto por **Andrej Karpathy** (gist `llm-wiki.md`, abril de 2026), construída e mantida por um agente de IA a partir da minha biblioteca de programação competitiva ([Jvrco/Competitive-Programming-Lib](https://github.com/Jvrco/Competitive-Programming-Lib)).

> **Ideia central:** em vez de o modelo redescobrir conhecimento dos códigos brutos a cada pergunta (como num RAG tradicional), o agente **compila e mantém** uma wiki estruturada em Markdown interligado, de modo que o conhecimento se acumule entre sessões.

---

## Navegação Rápida

- **[RELATORIO.md](RELATORIO.md)** — Relatório da atividade (origem do material bruto, estrutura adotada, evidências das operações e reflexões).
- **[index.md](index.md)** — Catálogo completo da wiki (ponto de entrada para consultas).
- **[AGENTS.md](AGENTS.md)** — Schema e protocolo que governam o agente (`ingest`, `query` com *write-back*, `lint`).
- **[log.md](log.md)** — Histórico cronológico *append-only* de todas as operações executadas.
- **[diario-de-uso.md](diario-de-uso.md)** — Diário de acompanhamento para 1 semana de uso prático.

---

## Arquitetura em 3 Camadas

```text
cp-llm-wiki/
├── AGENTS.md              # Schema do agente (regras, convenções, fluxos)
├── index.md               # Índice orientado a conteúdo (1 linha por página)
├── log.md                 # Audit trail cronológico (ingest / query / lint)
├── RELATORIO.md           # Relatório estruturado da atividade
├── diario-de-uso.md       # Diário de 7 dias de uso
├── raw/                   # Camada 1 (IMUTÁVEL): snapshot da Competitive-Programming-Lib (commit 49ccee9)
│   └── Competitive-Programming-Lib/
└── wiki/                  # Camada 2 (MANTIDA PELO AGENTE): conhecimento compilado
    ├── categorias/        # 8 mapas de domínio (64/64 arquivos catalogados)
    ├── padroes/           # 7 sínteses transversais (guias de decisão, trade-offs, adaptações)
    └── auditoria/         # 2 páginas de saúde (lint inicial + checklist pré-contest)
```

---

## Resultados da Compilação Inicial

- **100% de cobertura:** todos os **64 arquivos C++** (89,7 KB) em 8 categorias compilados em **17 páginas interligadas** (compatíveis com Obsidian).
- **Auditoria (`lint`) automática:** detectou **12 bugs/armadilhas reais** no código bruto (ex.: identidade de Pascal errada em `relations.cpp`, `prefix[0]` sem inicialização em `prefixsum2.cpp`, `freopen` hardcoded em `BFS.cpp`, `'a' -> 0` nos hashes) e **37 arquivos ausentes** do `contents.txt` que gera o PDF do caderno.
- **Acúmulo real (`query` + *write-back*):** consultas técnicas sobre adaptação de `segLazy.cpp` e checklist pré-contest foram persistidas de volta na wiki em vez de evaporarem ao fim da sessão.
