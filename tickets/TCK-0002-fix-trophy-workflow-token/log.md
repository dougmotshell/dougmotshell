# Log — TCK-0002

> Trilha append-only. Correção = nova entrada `CORRECTION`, nunca edição de entrada anterior.

## 2026-08-15 · ACTION · tech-lead

Triagem. Pedido classificado como `bug` / `automation`, tamanho P. Run 31884406883 falha no step
`Generate trophy SVG` com `exit code 3`. Levantamento do histórico (`gh run list`): **todas** as
execuções do `Generate Datas` estão vermelhas desde 2026-08-11 no recorte visível, e o último
commit da branch `output` é de **2026-07-22** — ou seja, o snake também está congelado há três
semanas. O `Update Languages Overview` está verde e não é afetado.

Delegado ao automation-engineer.

## 2026-08-15 · ACTION · automation-engineer

Investigação da causa raiz. A mensagem do log ("Check token, username and rate limits") é
genérica e vem do `catch` de `requestUserInfo` no `render_svg.ts` da action — não identifica o
campo que falhou.

Hipótese inicial (**descartada**): o `secrets.GITHUB_TOKEN` não conseguiria ler
`contributionsCollection` do usuário. Probe em CI (workflow temporário `debug-token.yml`,
disparado por push no branch do ticket, run 31902846895) devolveu `contributionsCollection`,
`followers` e `organizations` normalmente. Hipótese errada.

Segundo probe (run 31902919951) com a `queryUserAll` completa da action, mesmo token:

```json
"repositories": { "totalCount": 184, "nodes": [null, null, null, ...] },
"errors": [{ "type": "FORBIDDEN",
             "path": ["user","repositories","nodes",0,"stargazers"],
             "message": "Resource not accessible by integration" }]
```

Causa raiz confirmada: o installation token do GitHub Actions só enxerga o repositório onde roda,
então `stargazers` dos demais repos do usuário retorna `FORBIDDEN`. Sendo um campo não-nulável, o
GraphQL anula cada *node* inteiro; a action itera `nodes.reduce(... node.stargazers.totalCount)`,
estoura `TypeError` e sai com 3. A mesma query com um token de usuário devolve os 191 repos
completos — confirmando que é escopo de token, não rate limit nem username.

## 2026-08-15 · ACTION · automation-engineer

Correção em `.github/workflows/main.yml`:

| # | Mudança | Motivo |
|---|---|---|
| 1 | `token: ${{ secrets.TROPHY_TOKEN \|\| secrets.GITHUB_TOKEN }}` | PAT quando existir, sem quebrar sem ele |
| 2 | `continue-on-error: true` no step de troféus | falha do gerador não derruba o snake nem o deploy |
| 3 | Step de fallback baixando `trophies.svg` da branch `output` | `build_dir` substitui a branch inteira; sem o arquivo a imagem do README quebraria |
| 4 | `permissions: contents: write` | explicitar o que o deploy precisa |

Workflow temporário `debug-token.yml` removido do branch. Handoff → code-reviewer.

## 2026-08-15 · ACTION · code-reviewer

Revisão do diff. Pontos verificados:

- `secrets.X || secrets.Y` — expressão válida; segredo ausente avalia como string vazia (falsy). OK.
- `if: steps.trophy.outcome != 'success'` — usa `outcome` (resultado real) e não `conclusion`, que
  com `continue-on-error` seria sempre `success`. Correto.
- `curl -fsSL` sem `|| true`: se o fallback falhar, o job falha **antes** do deploy, deixando a
  branch `output` intacta. Falhar aqui é mais seguro que publicar um `dist` incompleto. OK.
- Nenhum segredo hardcoded; nenhum serviço pago introduzido (ADR-0004 preservado).
- Marcadores `LANGUAGES-START/END` e `README.md` não tocados.

Aprovado. Handoff → qa-validator.

## 2026-08-15 · ACTION · qa-validator

Validação end-to-end. `Generate Datas` disparado via `workflow_dispatch` no branch do ticket
(run 31903035597, 19s):

| Critério | Resultado |
|---|---|
| Job conclui com sucesso sem `TROPHY_TOKEN` | ✅ verde |
| Falha do gerador continua visível | ✅ `::warning::` na aba Actions |
| Branch `output` republicada | ✅ commit em 2026-08-15T19:07:57Z (antes: 2026-07-22) |
| Três arquivos presentes | ✅ snake claro e escuro (34646 B, regenerados de 33826 B) + `trophies.svg` (66481 B, preservado) |
| Imagens do README | ✅ nenhuma URL da branch `output` ficou sem arquivo |

Critérios 1–5 aprovados. Critério 6 depende do segredo `TROPHY_TOKEN`, que só o Douglas pode
criar — ticket fica `blocked-on-douglas` para esse item, com o pipeline já verde.

## 2026-08-15 · ACTION · qa-validator

Douglas mergeou o [PR #2](https://github.com/dougmotshell/dougmotshell/pull/2) (`ef2cead`).
Revalidação na branch `main` — run [31903263793](https://github.com/dougmotshell/dougmotshell/actions/runs/31903263793):
verde em 20s, warning do fallback presente, branch `output` republicada. O agendamento
(cron `0 0,12 * * *`) roda na `main`, então a próxima execução automática já sai verde.

Ticket **done** para os critérios 1–5. Handoff → docs-writer.

## 2026-08-15 · ACTION · docs-writer

Documentação atualizada após a entrega:

| Documento | Mudança |
|---|---|
| [ADR-0005](../../docs/adr/0005-resilient-output-branch-publishing.md) | novo — publicação resiliente da branch `output` (continue-on-error + fallback por artefato + warning visível) |
| [docs/adr/README.md](../../docs/adr/README.md) | índice com o ADR-0005 |
| [lessons.md](../../agents/memory/lessons.md) | L-001 (escopo do `GITHUB_TOKEN`) e L-002 (CI vermelho despercebido por três semanas) |
| [context/automation.md](../../agents/memory/context/automation.md) | `build_dir` substitui a branch inteira; limite do `GITHUB_TOKEN`; segredo `TROPHY_TOKEN` |
| [AGENTS.md](../../AGENTS.md) | regra 7 (segredos), estado atual, índice de ADRs |

Pendência aberta e **não** endereçada por este ticket: a seção de troféus do README usa `<img>`
simples, sem o `<picture>` claro/escuro exigido pelo [ADR-0003](../../docs/adr/0003-light-dark-theme-parity.md).
Merece ticket próprio (readme-designer).
