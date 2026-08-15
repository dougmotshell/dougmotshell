# TCK-0003: cards de GitHub Stats quebrados — migrar para instância própria

- **status:** blocked-on-douglas
- **owner:** automation-engineer
- **created:** 2026-08-15 · **by:** Douglas
- **type:** bug
- **size:** P

## Pedido original (verbatim)

> vi outro problema acontecendo no render o README [captura de tela dos dois cards da seção
> GitHub Stats exibindo "Something went wrong! ... Maximum retries exceeded / Please add an env
> variable called PAT_1 with your github token in vercel"]

## Requisito refinado

- Objetivo: os dois cards da seção **📊 GitHub Stats** (stats gerais e top languages) voltarem a
  renderizar, sem depender de instância pública de terceiro.
- Fora de escopo: demais seções do README (streak, activity graph, typing, waves) — todas
  verificadas e saudáveis.

## Diagnóstico

Os cards apontavam para `github-readme-stats-sigma-five.vercel.app`, uma instância pública de
terceiro do [github-readme-stats](https://github.com/anuraghazra/github-readme-stats). Ela está
sem token configurado e devolve o SVG de erro pedindo `PAT_1` — variável de ambiente **do
servidor dela**, não do nosso repositório. Nada a corrigir do nosso lado naquele arranjo.

A instância oficial (`github-readme-stats.vercel.app`) não é alternativa: responde
`DEPLOYMENT_PAUSED` — o projeto upstream estoura a cota gratuita do Vercel com frequência.

Varredura dos 42 recursos externos do README (todos os hosts, exceto links de navegação):

| Host | Situação |
|---|---|
| `github-readme-stats-sigma-five.vercel.app` (4 URLs + 2 no fallback) | ❌ erro `PAT_1` |
| `capsule-render.vercel.app`, `readme-typing-svg.demolab.com`, `streak-stats.demolab.com`, `github-readme-activity-graph.vercel.app`, `skillicons.dev`, `cdn.simpleicons.org`, `komarev.com` | ✅ HTTP 200 |

Problema isolado nos dois cards.

## Decisão

Douglas optou por **self-host no Vercel** (entre self-host, gerar no CI, trocar de instância
pública ou remover a seção). Mantém os cards idênticos, custo zero ([ADR-0004](../../docs/adr/0004-zero-cost-external-services.md))
e move o rate limit para uma cota própria — trocar por outra instância comunitária apenas adiaria
a mesma falha.

## Correção aplicada

As 6 URLs (3 por card: `prefers-color-scheme: dark`, `light` e `<img>` de fallback) passaram de
`github-readme-stats-sigma-five.vercel.app` para `github-readme-stats-sage-seven.vercel.app`.

Usado o **domínio de produção**, não o de deployment que veio com sufixo de build
(`...-leiahhiu8b.vercel.app`): o domínio de deployment congela num build específico e deixaria os
cards presos à versão atual do fork a cada redeploy.

## Pendência do Douglas

A instância própria está sem `PAT_1` efetivo: as primeiras requisições responderam (cota anônima
de 60/h do GitHub) e as seguintes passaram a devolver `Downtime due to GitHub API rate limiting`.
Com um PAT válido o limite seria de 5.000/h. Verificar, no painel do Vercel:

1. **Deployments → Redeploy** — variável adicionada após o build não entra no deploy corrente.
2. **Settings → Environment Variables** — `PAT_1` marcado para o ambiente **Production**.
3. Nome exato `PAT_1` e valor sem espaços nas pontas.

## Critérios de aceite

- [x] 1. Causa raiz identificada e isolada (nenhum outro recurso do README afetado).
- [x] 2. Cards apontam para instância própria, no domínio de produção.
- [x] 3. Paridade de temas preservada: 3 URLs por card (dark, light, fallback).
- [ ] 4. Os dois cards renderizam dados reais (bloqueado pelo `PAT_1`).
- [ ] 5. Renderização conferida nos temas claro e escuro do GitHub.

## Referências

- SPEC: [SPEC-001](../../docs/specs/spec-profile-readme.md) · ADRs: [0003](../../docs/adr/0003-light-dark-theme-parity.md), [0004](../../docs/adr/0004-zero-cost-external-services.md)
- Arquivos-alvo: `README.md` (seção `### 📊 GitHub Stats`)

## Resolução (preenchido ao fechar)

- Commits: · Evidência final (preview/run): · Docs atualizados:
