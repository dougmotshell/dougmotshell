# ADR-0001: O `README.md` é o produto (overview do usuário no GitHub)

- **Status:** aceito
- **Data:** 2026-07-19

## Contexto

O repositório `dougmotshell/dougmotshell` tem o mesmo nome do usuário — o caso especial em que o GitHub renderiza o `README.md` do repositório como **overview/vitrine do perfil** em https://github.com/dougmotshell. É a primeira coisa que recrutadores, colegas e visitantes veem. Não há aplicação, backend nem usuários finais além de quem visita o perfil.

## Decisão

Tratar o **`README.md` como o produto** deste repositório. Toda a infraestrutura (docs, ADRs, spec, fluxo de agentes, CI) existe para produzir e manter esse único artefato com qualidade e de forma automatizada. Métricas de sucesso são de comunicação (clareza, atualidade, boa renderização), não de software rodando.

## Consequências

- ✅ Escopo nítido: mudanças se avaliam por "melhora o que o visitante vê?".
- ✅ Justifica o rigor (spec, ADRs, tickets): o repo também é uma vitrine de **como** o Douglas trabalha.
- ⚠️ "Renderização real no GitHub, nos dois temas" é o critério de aceite final — não basta o markdown estar correto (ver [ADR-0003](0003-light-dark-theme-parity.md)).
- Obrigação: qualquer entregável estruturado novo tem uma [spec](../specs/spec-template.md); hoje há uma só ([SPEC-001](../specs/spec-profile-readme.md)).

## Alternativas rejeitadas

- **Tratar como repositório comum de código** — ignora que o artefato entregue é conteúdo renderizado, com pegadinhas próprias (sanitização de HTML, cache de CDN, temas).
