# Log de Operações — `cp-llm-wiki`

Registro cronológico *append-only* seguindo o padrão LLM Wiki (Karpathy, abril 2026).

## [2026-11-25] ingest | Compilação inicial da Competitive-Programming-Lib
- **Fonte:** `https://github.com/Jvrco/Competitive-Programming-Lib` clonada em `raw/Competitive-Programming-Lib/`.
- **Volume ingerido:** 64 arquivos em `Library/` (89,7 KB de C++ distribuídos em 8 categorias) + `contents.txt` e scripts de geração do caderno LaTeX.
- **Páginas criadas:**
  - 8 mapas de categoria em `wiki/categorias/` (`buscas`, `dp`, `geometria`, `grafos`, `range-queries`, `strings`, `teoria-dos-numeros`, `outros`).
  - 6 páginas de síntese transversal em `wiki/padroes/`.
  - `AGENTS.md`, `index.md` e `diario-de-uso.md`.

## [2026-11-25] lint | Auditoria inicial da base bruta e da wiki
- **Relatório:** `wiki/auditoria/lint-inicial.md`.
- **Achados principais:**
  - 12 bugs ou armadilhas concretas detectadas no código bruto (ex.: identidade de Pascal incorreta em `relations.cpp`, `prefix[0]` não inicializado em `prefixsum2.cpp`, `int mid` em busca `ll` em `cows.cpp`, `freopen` hardcoded em `BFS.cpp`, `'a' -> 0` nos hashes em `Hash*.cpp`, `double` no cross product de `ConvexHull.cpp`).
  - `contents.txt` desatualizado: 37 de 64 arquivos da pasta `Library/` não estão incluídos no gerador de PDF (incluindo 100% de `DP/` e `Strings/`).
  - 2 arquivos em `Library/Range/` sem extensão `.cpp` (`Range Xor Queries` e `RangeUpdateQueries`).
  - Identificados 2 estilos de autoria distintos convivendo na lib (`#define endl` + `main()` vs. `#define endll` + `solve()`).
  - 0 páginas órfãs na `wiki/`; 100% dos 64 arquivos de `raw/` cobertos e indexados.

## [2026-11-25] query | Adaptações de Segment Tree / Lazy Propagation (salvo em `wiki/padroes/adaptacoes-segtree-e-lazy.md`)
- **Consulta:** como adaptar `Range/segLazy.cpp` (Range Add + Range Min) para Range Sum e Range Assign, e como evitar conflito de indexação com `segtreewithcompression.cpp` (0-based).
- **Write-back:** criada `wiki/padroes/adaptacoes-segtree-e-lazy.md` e indexada em `index.md`.

## [2026-11-25] query | Checklist pré-contest e sincronização do PDF (salvo em `wiki/auditoria/checklist-pre-contest.md`)
- **Consulta:** consolidar correções prioritárias nos templates e arquivos ausentes no `contents.txt` antes de gerar o caderno PDF.
- **Write-back:** criada `wiki/auditoria/checklist-pre-contest.md` e indexada em `index.md`.

## [2026-11-25] ingest | Documentação de publicação e relatório (`README.md`, `RELATORIO.md`)
- **Snapshot bruto:** `raw/Competitive-Programming-Lib` fixado no commit `49ccee9` como snapshot imutável no repositório da wiki.
- **Arquivos criados:** `README.md` e `RELATORIO.md` consolidando o relato da atividade.

## [2026-11-26] query | Mapa reverso de problemas clássicos (salvo em `wiki/padroes/mapa-de-problemas.md`)
- **Consulta:** mapear todos os problemas identificáveis (CSES, Codeforces, AtCoder, SPOJ, Library Checker) para seus arquivos em `raw/Competitive-Programming-Lib/` e páginas da wiki.
- **Write-back:** criada `wiki/padroes/mapa-de-problemas.md` (~47 problemas mapeados) e indexada em `index.md`.

## [2026-11-26] ingest | Nota textual `raw/notas/erros-comuns-contest.md` + checklist de submissão
- **Fonte:** `raw/notas/erros-comuns-contest.md` (demonstrando ingestão de notas textuais além de código C++).
- **Integração:** criada `wiki/padroes/armadilhas-antes-de-submeter.md` cruzando a nota com `lint-inicial.md` e `conventions-e-estilos-da-lib.md`; atualizado `index.md`.

## [2026-11-26] lint | Verificação de integridade pós-expansão (19 páginas em `wiki/`)
- **Cobertura de `raw/`:** 64/64 arquivos C++ + 1/1 nota textual em `raw/notas/` (100%).
- **Páginas órfãs:** 0 (todas as 19 páginas em `wiki/` estão listadas em `index.md` e interligadas).
- **Wikilinks quebrados:** 0.
