# Contexto operacional — QA (validação do perfil)

> Documento **vivo** ([regras](../README.md)). Só conhecimento **não óbvio**. Toda entrada leva data.

## Pegadinhas conhecidas

- 2026-07-19 — Validar a **renderização real**, não o markdown-fonte: um `<picture>` com fonte errada renderiza no fonte mas quebra na tela. Usar o `/readme-check`, o preview do GitHub, ou um renderizador fiel ao GitHub.
- 2026-07-19 — Testar os **dois temas**: o GitHub não tem toggle de tema por README; alternar o tema da conta/navegador (ou inspecionar cada `<source media>`).
- 2026-07-19 — Imagem "quebrada" pode ser cache do camo/CDN, não erro real — conferir a URL do serviço diretamente antes de reprovar.

## Estado atual e decisões em vigor

- 2026-07-19 — Critérios recorrentes de aceite do perfil: (a) todos os links resolvem; (b) toda imagem renderiza em claro e escuro + fallback; (c) marcadores de linguagens presentes e tabela bem-formada; (d) CI verde quando o ticket toca script/workflow.

## Lições da área

- Ver [lessons.md](../lessons.md) filtrando por `qa`.
