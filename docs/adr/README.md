# ADRs — Decisões de Projeto

Registros de decisão no formato de [Architecture Decision Records](https://adr.github.io/) (Michael Nygard, 2011): cada decisão importante sobre **como este perfil é construído e mantido** fica documentada com contexto, decisão, evidência e consequências — para que o "porquê" não se perca e a decisão possa ser revisitada.

## Formato

```
# ADR-NNNN: Título
- Status: aceito | proposto | substituído por ADR-XXXX
- Data: AAAA-MM-DD

## Contexto      → o problema e as forças em jogo
## Decisão       → o que foi decidido, em voz ativa
## Consequências → efeitos positivos, negativos e obrigações
## Alternativas rejeitadas → e por quê
```

## Índice

| ADR | Decisão | Status |
|---|---|---|
| [0001](0001-github-profile-readme-as-product.md) | O `README.md` é o produto (overview do usuário no GitHub) | aceito |
| [0002](0002-auto-generated-language-badges.md) | Tabela de linguagens gerada por CI entre marcadores | aceito |
| [0003](0003-light-dark-theme-parity.md) | Paridade de temas claro/escuro em toda imagem via `<picture>` | aceito |
| [0004](0004-zero-cost-external-services.md) | Somente serviços externos gratuitos | aceito |
| [0005](0005-resilient-output-branch-publishing.md) | Publicação resiliente da branch `output` (fallback por artefato) | aceito |
