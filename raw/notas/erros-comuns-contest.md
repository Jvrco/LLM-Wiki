# Notas de Treino — Erros Comuns em Contest (Fonte Bruta)

Nota bruta adicionada em `raw/notas/` para demonstrar a operação `ingest` da LLM Wiki com material textual além de código `.cpp`:

1. **TLE por `endl` em problemas com muitas queries:** arquivos do Estilo B definem `#define endll '\n'` mas escrevem `cout << ans << endl;` (fazendo flush a cada linha).
2. **Confusão de indexação ao misturar SegTree com Compressão de Coordenadas:** esquecer que `segtreewithcompression.cpp` é 0-based enquanto `segtree.cpp` e `segLazy.cpp` são 1-based.
3. **Prioridade de lacunas para os próximos treinos:** implementar primeiro **KMP / Z-function** (para não depender só de Rolling Hash em Codeforces) e **Kruskal** (reaproveitando `DSU.cpp`).
