# AGENTS.md — Schema da LLM Wiki (`cp-llm-wiki`)

Este repositório implementa o padrão **LLM Wiki** proposto por Andrej Karpathy (abril de 2026): em vez de o modelo redescobrir conhecimento dos arquivos brutos a cada pergunta (como num RAG tradicional), o agente **compila e mantém** uma base estruturada em Markdown que acumula conhecimento entre sessões.

---

## 1. Arquitetura em 3 Camadas

1. **`raw/` (Fontes Brutas — Imutável)**
   - Contém o material original (`raw/Competitive-Programming-Lib/`).
   - **Regra absoluta:** o agente **nunca** edita, renomeia ou apaga arquivos em `raw/`. Eles são a fonte da verdade.
2. **`wiki/` (Base Compilada — Mantida pelo Agente)**
   - Coleção interligada de páginas Markdown com wikilinks (`[[nome-da-pagina]]`) e referências diretas aos arquivos em `raw/`.
   - Subdiretórios:
     - `wiki/categorias/` — Mapas de domínio correspondentes às pastas da lib (inventário completo + classificação template vs. problema resolvido).
     - `wiki/padroes/` — Sínteses transversais que conectam técnicas, trade-offs e decisões entre múltiplas categorias.
     - `wiki/auditoria/` — Relatórios de saúde (`lint`), bugs detectados no código bruto, inconsistências e lacunas de cobertura.
3. **Arquivos de Controle na Raiz**
   - `AGENTS.md` — Este schema (regras, convenções e operações).
   - `index.md` — Catálogo orientado a conteúdo listando todas as páginas da wiki com resumo de 1 linha. **Sempre leia `index.md` antes de responder uma consulta.**
   - `log.md` — Registro cronológico *append-only* de todas as operações (`ingest`, `query`, `lint`).
   - `diario-de-uso.md` — Registro da atividade prática (origem do material, estrutura adotada e diário de 1 semana de uso).

---

## 2. Convenções das Páginas da Wiki

- **Frontmatter YAML** no topo de cada página em `wiki/`:
  ```yaml
  ---
  titulo: Nome da Página
  tipo: categoria | padrao | auditoria | problema
  tags: [tag1, tag2]
  fontes:
    - raw/Competitive-Programming-Lib/Library/...
  atualizado: YYYY-MM-DD
  ---
  ```
- **Links internos:** use wikilinks `[[caminho/sem-extensao|Rótulo]]` (compatível com Obsidian) para conectar conceitos relacionados.
- **Citações ao código bruto:** cite o caminho relativo exato em `raw/Competitive-Programming-Lib/...` e, quando relevante, a função ou linha.
- **Distinção explícita:** sempre diferencie o que é **Template reutilizável** do que é **Solução de problema específico** (anotando o problema original quando identificável, ex.: CSES, Codeforces, SPOJ, AtCoder).
- **Idioma:** Português (PT-BR), mantendo termos técnicos consagrados em inglês (ex.: *Segment Tree*, *Lazy Propagation*, *Meet in the Middle*, *Digit DP*).

---

## 3. Operações Principais do Agente

### A. `ingest` (Ingerir novo material)
Quando o usuário adicionar novos códigos, editoriais, notas de aula ou atualizar o repositório em `raw/`:
1. Leia o(s) arquivo(s) novo(s) ou modificado(s) em `raw/`.
2. Atualize a página correspondente em `wiki/categorias/` (ou crie uma nova se surgir categoria inédita).
3. Atualize as páginas transversais afetadas em `wiki/padroes/` (ex.: se entrou um KMP, atualize `wiki/padroes/hashing-e-trie.md` ou crie `wiki/padroes/string-matching.md`).
4. Verifique se o novo material resolve ou introduz algum item em `wiki/auditoria/lint-inicial.md`.
5. Atualize `index.md` se páginas foram criadas ou alteradas significativamente.
6. Adicione uma entrada no final de `log.md` no formato:
   `## [YYYY-MM-DD] ingest | Descrição curta`

### B. `query` (Consultar e acumular conhecimento)
Quando o usuário fizer uma pergunta técnica (ex.: *"qual estrutura da minha lib uso para range update + range min?"*, *"tenho algum código de bipartição?"*, *"como adaptar minha segtree para soma?"*):
1. Leia `index.md` primeiro para localizar as páginas relevantes da `wiki/`.
2. Abra as páginas da `wiki/` necessárias (e consulte `raw/` apenas se precisar confirmar uma linha exata de código).
3. Responda de forma direta, citando os arquivos da lib e eventuais *gotchas* já documentados na wiki.
4. **Acúmulo (Write-back):** se a resposta gerar uma comparação nova, uma adaptação útil de template ou uma análise que valha preservar, salve-a como nova página (ou seção) em `wiki/padroes/` e registre em `index.md` e `log.md`:
   `## [YYYY-MM-DD] query | Tópico da consulta (salvo em ...)`

### C. `lint` (Auditoria de saúde da wiki)
Periodicamente (ou quando o usuário pedir `lint`):
1. Verifique se todos os arquivos em `raw/Competitive-Programming-Lib/Library/` estão catalogados na `wiki/`.
2. Verifique se há páginas órfãs (não listadas em `index.md` ou sem links de entrada).
3. Verifique contradições entre páginas da wiki ou entre a wiki e o código em `raw/`.
4. Atualize o relatório em `wiki/auditoria/` e registre em `log.md`:
   `## [YYYY-MM-DD] lint | Resumo dos achados`
