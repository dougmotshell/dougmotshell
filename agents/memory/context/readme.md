# Contexto operacional — README (conteúdo + visual do perfil)

> Documento **vivo** ([regras](../README.md)). Só conhecimento **não óbvio**. Toda entrada leva data.

## Pegadinhas conhecidas

- 2026-07-19 — GitHub **sanitiza CSS e a maioria dos atributos de estilo** no README; alinhamento/centralização se faz com `<div align="center">`, `<td align="center">` e `<picture>`, não com `style="..."`.
- 2026-07-19 — Alternância de tema **só** via `<picture>` + `<source media="(prefers-color-scheme: dark|light)">` + `<img>` de fallback. Não existe "detectar tema" por JS no README.
- 2026-07-19 — Serviços de imagem (capsule-render, readme-typing-svg, github-readme-stats, shields.io) fazem **cache** no CDN do GitHub (camo). Mudança na URL pode demorar a refletir; para conferir, abrir a URL do serviço direto.

## Estado atual e decisões em vigor

- 2026-07-19 — Seções do README (ordem): header wave → typing SVG → profile views/followers → About Me → Featured Projects → GitHub Stats → Streak → Trophies → Tech Stack → Contribution Activity → Snake → Connect → **Most Used Languages (auto)** → footer wave.
- 2026-07-19 — A seção de linguagens é gerada por CI entre `<!-- LANGUAGES-START -->` e `<!-- LANGUAGES-END -->` — não editar à mão ([ADR-0002](../../../docs/adr/0002-auto-generated-language-badges.md)).

## Lições da área

- Ver [lessons.md](../lessons.md) filtrando por `readme`.
