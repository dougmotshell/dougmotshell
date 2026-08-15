# Log — TCK-0003

> Trilha append-only. Correção = nova entrada `CORRECTION`, nunca edição de entrada anterior.

## 2026-08-15 · ACTION · tech-lead

Triagem. Douglas reportou, com captura de tela, os dois cards da seção **📊 GitHub Stats**
exibindo `Something went wrong! ... Please add an env variable called PAT_1 with your github
token in vercel`. Classificado como `bug` / `visual+automation`, tamanho P.

A mensagem cita uma variável de ambiente, o que sugere configuração faltando neste repositório —
não é o caso: `PAT_1` é variável do **servidor** que gera o card. Delegado ao automation-engineer
para confirmar antes de qualquer mudança no README.

## 2026-08-15 · ACTION · automation-engineer

Diagnóstico por requisição direta aos serviços:

| Alvo | Resultado |
|---|---|
| `github-readme-stats-sigma-five.vercel.app` (instância em uso) | SVG de erro pedindo `PAT_1` |
| `github-readme-stats.vercel.app` (instância oficial) | `DEPLOYMENT_PAUSED` — cota gratuita do upstream esgotada |

Varredura completa dos 42 recursos externos do README (agrupados por host, excluídos links de
navegação): apenas os 6 URLs do github-readme-stats falham. `capsule-render`, `readme-typing-svg`,
`streak-stats`, `github-readme-activity-graph`, `skillicons`, `cdn.simpleicons` e `komarev`
respondem 200. Um falso positivo inicial no `skillicons.dev` era a home do serviço (CSS com a
palavra "error"), não a API de ícones.

Conclusão: instância de terceiro morta. Como [ADR-0004](../../docs/adr/0004-zero-cost-external-services.md)
manda propor substituto em vez de deixar imagem quebrada, quatro caminhos foram apresentados ao
Douglas (self-host, gerar no CI como snake/troféus, outra instância pública, remover a seção).
Escolha: **self-host no Vercel**.

## 2026-08-15 · ACTION · automation-engineer

Douglas informou primeiro `dougmotshell.vercel.app` — respondia `404 NOT_FOUND` da plataforma,
inclusive na raiz, indicando domínio sem deployment de produção associado (era outro projeto da
conta dele). Depois de refeito o import no Vercel, veio
`github-readme-stats-sage-seven-leiahhiu8b.vercel.app`.

Esse segundo endereço funciona, mas é o **domínio de deployment** (o sufixo `-leiahhiu8b` é o
hash do build): fica preso àquele build e não acompanha redeploys. Testado o domínio de produção
correspondente, `github-readme-stats-sage-seven.vercel.app` — também responde 200. Adotado o de
produção.

Trocadas as 6 URLs no `README.md` (3 por card: dark, light, fallback `<img>`) via substituição de
host; diff confere 6 inserções e 6 remoções, nada além do host alterado. Paridade de temas do
[ADR-0003](../../docs/adr/0003-light-dark-theme-parity.md) preservada.

## 2026-08-15 · ACTION · automation-engineer

Validação da instância nova revelou problema no deploy do Douglas. As primeiras requisições
retornaram SVG válido (7744 B com "Total Stars", 6665 B com "Most Used Languages"); as seguintes
passaram a devolver 767 B com:

```
Something went wrong!
Downtime due to GitHub API rate limiting
```

Interpretação: a instância está operando **sem token** — cota anônima do GitHub (60 req/h),
esgotada pelas próprias chamadas de teste. Com `PAT_1` válido o limite seria 5.000/h e seis
requisições não arranhariam a cota. Causas prováveis, nesta ordem: variável adicionada após o
build (exige redeploy), variável não marcada para o ambiente Production, ou nome/valor incorreto.

Ticket fica `blocked-on-douglas`. PR **não** aberto de propósito: mandar a mudança para a `main`
agora publicaria uma seção que ainda renderiza erro no perfil público. O branch
`tck-0003-selfhost-stats-cards` guarda o trabalho até a revalidação.
