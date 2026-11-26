---
titulo: Strings
tipo: categoria
tags: [strings, rolling-hash, trie, binary-trie, xor]
fontes:
  - raw/Competitive-Programming-Lib/Library/Strings/Hash.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Hash2.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Hash3.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/MostWordsWithPrefix.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Trie.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/TrieXorMin.cpp
atualizado: 2026-11-25
---

# Strings

Mapa compilado da pasta `Library/Strings/` (6 arquivos). **Atenção:** nenhum destes 6 arquivos está no `contents.txt` atual da lib.

Síntese técnica e comparativa em [[wiki/padroes/hashing-e-trie|Hashing Polinomial e Tries]].

---

## Inventário

| Arquivo | Tipo | Algoritmo / Problema | Complexidade | Observações |
|---|---|---|---|---|
| `Strings/Hash.cpp` | Template / Problema | **Polynomial Rolling Hash** com `__int128`: conta ocorrências do padrão `p` em `s` (CSES *String Matching*). | $O(|s| + |p|)$ | Snippet `solve()` sem `main()`. |
| `Strings/Hash2.cpp` | Problema | **Bordas de string** via Rolling Hash: encontra todos os tamanhos de prefixo que também são sufixo (CSES *Finding Borders*). | $O(n)$ | Declara `N` (2º módulo), mas usa apenas `M`. |
| `Strings/Hash3.cpp` | Problema | **Períodos de string** via Rolling Hash: testa blocos de tamanho $i+1$ + resto final (CSES *Finding Periods*). | $O(n \log n)$ (série harmônica) | Snippet `solve()` sem `main()`. |
| `Strings/Trie.cpp` | Template | **Trie de strings** (`map<int,int> next` + `sub_cnt`): inserção e contagem de quantas strings têm prefixo `s`. | $O(|s| \log \Sigma)$ | Único da pasta com `int main()`. |
| `Strings/MostWordsWithPrefix.cpp` | Problema | **Trie com pré-ordenação**: retorna a palavra mais frequente (menor lexicograficamente em empate) para cada prefixo consultado. | $O(\sum |s| \log \Sigma)$ | Insere do pior para o melhor sobrescrevendo `tr[cur].str`. |
| `Strings/TrieXorMin.cpp` | Template | **Binary Bitwise Trie (30 bits)** com `add`, `remove` (limpando nós vazios) e `query(x)` para **XOR mínimo** (Library Checker *Set Xor-Min*). | $O(30)$ por operação | Mantém `set<int>` externo para evitar duplicatas. |

---

## Detalhes e Armadilhas (*Gotchas*)

- **Armadilha crítica nos 3 arquivos `Hash*.cpp` — mapeamento `'a' -> 0`:**
  Todos usam `s[i] - 'a'` em vez de `s[i] - 'a' + 1`. Isso faz com que `"a"`, `"aa"`, `"aaa"` tenham todas hash `0`! Sempre use `(s[i] - 'a' + 1)` ao adaptar para problemas com substrings de tamanhos variáveis.
- **Quase-overflow em `pref[i - 1] * K` nos `Hash*.cpp`:**
  Os códigos definem `mod_mul` com `__int128`, mas só o chamam na subtração final (`mod_mul(pref[l-1], powers[r-l+1], M)`). Na construção de `pref[i]` e `powers[i]`, fazem `pref[i-1] * K` em `ll` puro! Com `M = 999999900409` ($\approx 10^{12}$) e `K = 1000213` ($\approx 10^6$), o produto chega a $10^{18}$ (dentro de `LLONG_MAX` $\approx 9.2 \times 10^{18}$, mas sem margem se trocar `M` ou `K`). O seguro é usar `mod_mul` também no loop de pré-cálculo.
- **Hash simples vs. duplo:** `Hash2.cpp` e `Hash3.cpp` declaram um segundo primo `N = 999999900637`, mas nunca o usam. Como `M` é $\approx 10^{12}$ (primo grande), o risco de colisão aleatória é baixo, mas em Codeforces um módulo fixo conhecido pode ser hackeado.
- **`Trie.cpp` e `TrieXorMin.cpp` usam `map<int, int>`:** consome menos memória que `int next[26]` em alfabetos grandes, mas tem constante maior; em `TrieXorMin.cpp` (alfabeto binário $\{0, 1\}$), trocar `map<int, int>` por `int next[2] = {-1, -1}` deixa a estrutura muito mais rápida e econômica em memória.

---

## Lacunas nesta Categoria

Ausentes na lib atual: **KMP** (função $\pi$), **Z-function** (alternativa determinística a `Hash.cpp`, `Hash2.cpp` e `Hash3.cpp` sem risco de colisão), **Manacher** (palíndromos) e **Aho-Corasick**.

---

## Páginas Relacionadas

- [[wiki/padroes/hashing-e-trie|Hashing Polinomial e Tries]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
