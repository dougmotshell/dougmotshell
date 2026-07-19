# Contexto operacional — Automation (script + CI)

> Documento **vivo** ([regras](../README.md)). Só conhecimento **não óbvio**. Toda entrada leva data.

## Pegadinhas conhecidas

- 2026-07-19 — `generate_languages.py` reescreve o README com `content.split(start_tag)[0]` + tabela + `content.split(end_tag)[-1]`. Se os marcadores forem duplicados/removidos, o split corrompe o arquivo. Preservar exatamente um par de marcadores.
- 2026-07-19 — O script **ignora forks** (`if repo.get("fork"): continue`) e agrega bytes por linguagem em todos os repos públicos do usuário. `LANG_CONFIG` define cor/logo; linguagem fora do config cai no default cinza `555555`.
- 2026-07-19 — `update-languages.yml` faz `git pull --rebase origin main` antes do push para não conflitar com commits concorrentes; roda em cron `0 0,12 * * *` + `workflow_dispatch`.
- 2026-07-19 — `main.yml` publica `dist/` (snake + troféus) na branch `output` via `crazy-max/ghaction-github-pages`; usa `Platane/snk` e `Erik-Donath/github-profile-trophy`.

## Estado atual e decisões em vigor

- 2026-07-19 — Único segredo: `GITHUB_TOKEN` (fornecido pelas Actions). `GITHUB_USERNAME` vem de `github.repository_owner`. Custo zero ([ADR-0004](../../../docs/adr/0004-zero-cost-external-services.md)).
- 2026-07-19 — Actions de terceiros devem ficar com versão fixada (evitar `@main`).

## Lições da área

- Ver [lessons.md](../lessons.md) filtrando por `automation`.
