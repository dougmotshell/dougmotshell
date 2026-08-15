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

Validação end-to-end pendente da execução real do workflow corrigido na branch `main`.
