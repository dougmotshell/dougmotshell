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

## 2026-08-15 · CORRECTION · automation-engineer

**A entrada anterior partiu de uma premissa errada.** Assumi que
`github-readme-stats-sage-seven.vercel.app` (sem o sufixo `-leiahhiu8b`) era o domínio de
produção do projeto do Douglas, tratando o sufixo como hash de build. Errado nos dois pontos:

- `github-readme-stats-sage-seven.vercel.app` pertence a **outra conta** — outro fork público
  qualquer, também sem token, também em rate limit. O README chegou a ser apontado para uma
  instância de terceiro, exatamente o problema que este ticket existe para eliminar.
- `github-readme-stats-sage-seven-leiahhiu8b.vercel.app` **é** o domínio de produção do projeto
  dele. O Vercel compõe `<projeto>-<palavras>-<sufixo>` quando o nome simples já está tomado por
  outra conta — e `github-readme-stats` e `...-sage-seven` já estavam.

O que induziu ao erro: a instância de terceiro respondeu 200 nos primeiros testes (tinha cota
anônima sobrando) e só depois passou a devolver rate limit, o que parecia confirmar "domínio
certo, token faltando". O diagnóstico de `PAT_1` não configurado, na entrada anterior, era falso
— o `PAT_1` do Douglas sempre esteve correto.

Lição: **domínio `.vercel.app` sem escopo não prova propriedade.** A lista de Domains do projeto,
no painel, é a única fonte confiável; deve ser pedida antes de editar qualquer URL.

## 2026-08-15 · ACTION · automation-engineer

Douglas enviou a lista de Domains do deployment. Verificação dos quatro candidatos:

| Domínio | HTTP | Conteúdo |
|---|---|---|
| `...-sage-seven-leiahhiu8b.vercel.app` | 200 | 7765 B — Rank B, 38 stars, 540 commits, 47 PRs |
| `...-git-master-douglas-matos-da-silvas-projects.vercel.app` | 302 | redirect de login (proteção do Vercel) |
| `...-1cfiugty9-douglas-matos-da-silvas-projects.vercel.app` | 302 | idem |
| `...-sage-seven.vercel.app` | 200 | 767 B — rate limit (terceiro) |

Os domínios com escopo `-douglas-matos-da-silvas-projects` não servem ao README: exigem
autenticação e devolveriam redirect para o renderizador do GitHub.

README corrigido para `github-readme-stats-sage-seven-leiahhiu8b.vercel.app` nas 6 URLs.

## 2026-08-15 · ACTION · qa-validator

Validação das 6 URLs exatas do README, com os parâmetros reais:

| URL | Resultado |
|---|---|
| stats — dark / light / fallback | 7744 B, "Douglas Matos da Silva's GitHub Stats, Rank: B" |
| top-langs — dark / light / fallback | 6665 B, "Most Used Languages" |

Paridade de temas ([ADR-0003](../../docs/adr/0003-light-dark-theme-parity.md)) conferida no SVG
servido: `fill="#0d1117"` no tema escuro, `fill="#ffffff"` no claro. Três URLs por card (dark,
light, `<img>` de fallback) preservadas.

Critérios 1–5 aprovados. Ticket **done**.
