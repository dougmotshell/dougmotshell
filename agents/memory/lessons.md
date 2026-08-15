# Lições aprendidas (append-only)

> Registro permanente de erros cometidos e como evitá-los — a memória que impede o mesmo erro duas vezes. Formato e gatilhos na seção ["Memória persistente"](../handoff-protocol.md#memória-persistente-lições-e-contexto) do protocolo. **Append-only**: lição superada = nova lição referenciando a antiga, nunca edição.

## [L-001] 2026-08-15 — automation — `GITHUB_TOKEN` não lê dados de outros repositórios do usuário

- Contexto: TCK-0002 — workflow `Generate Datas` falhando no step de geração dos troféus.
- Erro: `exit code 3` com a mensagem genérica `Failed to fetch user info. Check token, username and rate limits.` — que aponta para três causas erradas.
- Causa raiz: `secrets.GITHUB_TOKEN` é um *installation token* com escopo restrito ao repositório onde a Action roda. A query GraphQL pedia `stargazers` de **todos** os repos do usuário e recebia `FORBIDDEN — Resource not accessible by integration`; sendo campo não-nulável, o GraphQL anulou cada node inteiro (`nodes: [null, ...]`) e a action estourou `TypeError` iterando sobre eles.
- Como evitar: qualquer ferramenta que leia dados **do perfil inteiro** (repos, stars, contribuições agregadas) precisa de PAT dedicado — o `GITHUB_TOKEN` não serve, mesmo quando o README da action diz que sim. Antes de aceitar a mensagem de erro de uma action de terceiro, rodar a query crua no CI com o mesmo token e inspecionar o campo `errors` da resposta GraphQL: `data` parcial + `errors` é o padrão que produz esses crashes silenciosos.
- Refs: `.github/workflows/main.yml`, [ADR-0005](../../docs/adr/0005-resilient-output-branch-publishing.md), [ticket](../../tickets/TCK-0002-fix-trophy-workflow-token/ticket.md), runs 31884406883 (falha) e 31902919951 (probe).

## [L-002] 2026-08-15 — automation — CI vermelho por três semanas sem ninguém notar

- Contexto: TCK-0002 — ao investigar a falha do dia, o histórico mostrou que **toda** execução agendada do `Generate Datas` falhava desde 2026-07-22.
- Erro: a branch `output` ficou congelada nessa data; o snake parou de atualizar junto com os troféus, e o perfil seguiu exibindo dados velhos sem sinal visível.
- Causa raiz: um único step falho abortava o job inteiro antes do deploy, e nada no perfil denuncia artefato desatualizado (a imagem antiga continua renderizando normalmente).
- Como evitar: ao investigar uma falha de CI, sempre rodar `gh run list` e olhar **desde quando** falha — o run reportado costuma ser o mais recente, não o primeiro. E agrupar geradores independentes com `continue-on-error` + fallback, para que um quebrado não leve os outros ([ADR-0005](../../docs/adr/0005-resilient-output-branch-publishing.md)).
- Refs: [log do ticket](../../tickets/TCK-0002-fix-trophy-workflow-token/log.md), `.github/workflows/main.yml`.
