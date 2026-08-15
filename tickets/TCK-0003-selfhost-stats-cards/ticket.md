# TCK-0003: cards de GitHub Stats quebrados — migrar para instância própria

- **status:** done
- **owner:** qa-validator
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
`github-readme-stats-sigma-five.vercel.app` para
`github-readme-stats-sage-seven-leiahhiu8b.vercel.app` — o domínio de produção do projeto do
Douglas, conferido na lista de Domains do painel.

Atenção para quem mexer nisso depois: `github-readme-stats-sage-seven.vercel.app` (mesmo nome sem
o sufixo) pertence a **outra conta** e está em rate limit. O Vercel compõe
`<projeto>-<palavras>-<sufixo>` quando o nome simples já está tomado, então sufixo comprido não
significa "domínio de build descartável". Ver a entrada `CORRECTION` no [log](log.md).

## Sobre o `PAT_1`

Houve um falso alarme de `PAT_1` mal configurado durante a investigação: o rate limit observado
vinha da instância de terceiro, não do deploy do Douglas. O `PAT_1` dele sempre esteve correto —
`Production and Preview`, e o deploy responde com dados reais.

## Critérios de aceite

- [x] 1. Causa raiz identificada e isolada (nenhum outro recurso do README afetado).
- [x] 2. Cards apontam para instância própria, no domínio de produção.
- [x] 3. Paridade de temas preservada: 3 URLs por card (dark, light, fallback).
- [x] 4. Os dois cards renderizam dados reais (Rank B, 38 stars, 540 commits, 47 PRs).
- [x] 5. Cores conferidas no SVG servido: `#0d1117` no tema escuro, `#ffffff` no claro.

## Referências

- SPEC: [SPEC-001](../../docs/specs/spec-profile-readme.md) · ADRs: [0003](../../docs/adr/0003-light-dark-theme-parity.md), [0004](../../docs/adr/0004-zero-cost-external-services.md)
- Arquivos-alvo: `README.md` (seção `### 📊 GitHub Stats`)

## Resolução

- Commits: branch `tck-0003-selfhost-stats-cards`.
- Evidência final: as 6 URLs do README respondem SVG com dados reais (7744 B no card de stats,
  6665 B no de linguagens), com as cores corretas em cada tema.
- Docs pendentes: a lição sobre identificação de domínio Vercel (L-003) entra em
  [lessons.md](../../agents/memory/lessons.md) **após** o merge do PR #3 — aquele PR reescreve o
  bloco de placeholder do arquivo, e adicionar a lição aqui em paralelo geraria conflito bobo.
