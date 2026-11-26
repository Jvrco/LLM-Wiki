---
titulo: Geometria Computacional
tipo: categoria
tags: [geometria, convex-hull, produto-vetorial, distancia-ponto-reta]
fontes:
  - raw/Competitive-Programming-Lib/Library/Geometria/ConvexHull.cpp
  - raw/Competitive-Programming-Lib/Library/Geometria/Hurricane.cpp
  - raw/Competitive-Programming-Lib/Library/Geometria/PointLocation.cpp
  - raw/Competitive-Programming-Lib/Library/Geometria/Triangulo.cpp
atualizado: 2026-11-25
---

# Geometria Computacional

Mapa compilado da pasta `Library/Geometria/` (4 arquivos). Todos os 4 estão incluídos no `contents.txt`.

---

## Inventário

| Arquivo | Tipo | Algoritmo / Problema | Complexidade | Observações |
|---|---|---|---|---|
| `Geometria/ConvexHull.cpp` | Template | **Convex Hull** (Monotone Chain / Andrew) com struct `pt` (`+`, `-`, `*`, `len`, `cross`, `<`, `==`) e flag `include` para pontos colineares na borda. | $O(n \log n)$ | Snippet `solve()` sem `main()`. |
| `Geometria/PointLocation.cpp` | Template / Problema | **Orientação de 3 pontos** via produto vetorial `(x2-x1)*(y3-y1) - (y2-y1)*(x3-x1)` $\rightarrow$ `LEFT` / `RIGHT` / `TOUCH` (CSES *Point Location Test*). | $O(1)$ por query | Inteiro exato (`ll`). |
| `Geometria/Hurricane.cpp` | Problema | **Distância ao quadrado de ponto à reta** (`sqd`) usando área do paralelogramo $\frac{\text{cross}^2}{\text{len}^2}$, com tolerância `1e-15` para empates. | $O(m)$ por caso | Usa `double`; trata reta degenerada (`lensq == 0`). |
| `Geometria/Triangulo.cpp` | Problema | Contagem de triângulos retângulos com vértices nas retas $y = 0$ e $y = 1$ (Codeforces *Satyam and Counting*) usando `unordered_set<ll>`. | $O(n)$ médio | Conta ângulos retos verticais/horizontais e diagonais $45^\circ$. |

---

## Detalhes e Armadilhas (*Gotchas*)

- **`ConvexHull.cpp` — Perda de precisão no `orientation()`:** na linha 48, `double v = AB.cross(BC);` converte o produto vetorial `ll` para `double`. Para coordenadas até $10^9$, `cross` chega a $2 \times 10^{18}$, onde `double` (53 bits de mantissa $\approx 9 \times 10^{15}$) perde precisão e pode inverter o sinal ou gerar falso zero! **Correção:** usar `ll v = AB.cross(BC);` (ou `__int128` se $|x|, |y| > 10^9$).
- **`Hurricane.cpp` — Tolerância `1e-15`:** comparar `abs(distsq[i] - mindist) < 1e-15` em `double` pode falhar para coordenadas grandes (onde a precisão relativa de `double` é $\approx 10^{-15} \cdot \text{valor}$). Em geometria exata, comparar distâncias ao quadrado sem divisão usando multiplicação cruzada inteira elimina erro de ponto flutuante.
- **`Triangulo.cpp`:** usa `unordered_set<ll>`, vulnerável a *anti-hash test* no Codeforces (prefira `set` ou custom hash se tomar TLE).
- **Boilerplate residual:** `Hurricane.cpp`, `PointLocation.cpp` e `Triangulo.cpp` declaram `dx[4]`, `dy[4]` e `#define MOD 1000000007` sem usá-los (ver [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]).

---

## Lacunas nesta Categoria

Para expandir a lib no futuro: interseção de segmentos, área de polígono (*Shoelace*), ponto dentro de polígono (*Ray Casting* / *Winding Number*).

---

## Páginas Relacionadas

- [[wiki/auditoria/lint-inicial|Relatório de Lint Inicial]]
- [[wiki/padroes/conventions-e-estilos-da-lib|Convenções e Estilos da Lib]]
