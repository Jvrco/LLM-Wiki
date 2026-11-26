---
titulo: Hashing Polinomial e Tries
tipo: padrao
tags: [strings, rolling-hash, trie, binary-trie, colisao]
fontes:
  - raw/Competitive-Programming-Lib/Library/Strings/Hash.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Hash2.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Hash3.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/MostWordsWithPrefix.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/Trie.cpp
  - raw/Competitive-Programming-Lib/Library/Strings/TrieXorMin.cpp
atualizado: 2026-11-25
---

# Hashing Polinomial e Tries

Comparação das duas famílias de estruturas em [[wiki/categorias/strings|Strings]] e cuidados críticos ao reutilizar os códigos da lib.

---

## 1. Polynomial Rolling Hash (`Hash.cpp`, `Hash2.cpp`, `Hash3.cpp`)

Todos os três arquivos compartilham o mesmo núcleo:
- **Módulo:** `M = 999999900409` (primo $\approx 10^{12}$).
- **Base:** `K = 1000213` (primo $\approx 10^6$).
- **Consulta de substring $s[l \dots r]$ em $O(1)$:**
  $$\text{hash}(l, r) = \left(\text{pref}[r] - \text{pref}[l-1] \cdot K^{r-l+1}\right) \bmod M$$
  usando `mod_mul` com `__int128`.

### Aplicações já prontas na lib
1. **String Matching (`Hash.cpp`):** janela deslizante de tamanho $|p|$ comparando `subHash == pHash` em $O(n + m)$.
2. **Bordas (`Hash2.cpp`):** compara `pref[i]` com o sufixo de mesmo tamanho `[n-1-i .. n-1]` em $O(n)$.
3. **Períodos (`Hash3.cpp`):** testa cada candidato de período $d = i + 1$ pulando em blocos de tamanho $d$ (custo total $O(n \log n)$ pela série harmônica $\sum n/d$).

### 2 Correções Obrigatórias antes de usar em Contest
1. **Troque `s[i] - 'a'` por `(s[i] - 'a' + 1)`:** com `'a' -> 0`, `"a"` e `"aa"` têm o mesmo hash (`0`), gerando falsos positivos sempre que comprimentos diferirem ou em comparações com prefixos de `'a'`.
2. **Use `mod_mul` também no pré-cálculo:** atualmente `pref[i-1] * K` e `powers[i-1] * K` multiplicam `ll * ll` diretamente ($\approx 10^{18}$, no limite de `LLONG_MAX`).

---

## 2. Tries (`Trie.cpp`, `MostWordsWithPrefix.cpp`, `TrieXorMin.cpp`)

| Variante | Arquivo | Chave nos nós | Operações | Caso de uso |
|---|---|---|---|---|
| **Trie de Prefixos** | `Strings/Trie.cpp` | `map<int,int> next`, `sub_cnt` | `add(s)`, `query(prefix)` | Contar quantas palavras começam com `s`. |
| **Trie com Melhor Resposta por Prefixo** | `Strings/MostWordsWithPrefix.cpp` | `map<int,int> next`, `int str` | `add(s, id)`, `query(prefix)` | Pré-ordena palavras (pior $\to$ melhor) e sobrescreve `str` no caminho, respondendo em $O(|s|)$ a palavra mais frequente com aquele prefixo. |
| **Binary Bitwise Trie (30 bits)** | `Strings/TrieXorMin.cpp` | `map<int,int> next` ($\{0, 1\}$), `sub_cnt` | `add(x)`, `remove(x)`, `query(x)` | **XOR mínimo** (tenta seguir o mesmo bit `id`; se ausente, vai para `id ^ 1` e soma `1 << b`). Para **XOR máximo**, basta tentar `id ^ 1` primeiro! |

### Dica de Performance
Em `TrieXorMin.cpp`, cada nó tem no máximo 2 filhos (`0` e `1`). Substituir `map<int, int> next` por `int next[2] = {0, 0}` reduz drasticamente o uso de memória e o tempo de execução (fator $\sim 5\times$ a $10\times$ mais rápido).

---

## Páginas Relacionadas

- [[wiki/categorias/strings|Strings]]
- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
