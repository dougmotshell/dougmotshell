# TCK-0002: pipeline "Generate Datas" falhando na geração dos troféus

- **status:** done (critério 6 pendente do Douglas)
- **owner:** qa-validator
- **created:** 2026-08-15 · **by:** Douglas
- **type:** bug
- **size:** P

## Pedido original (verbatim)

> pipeline falhando resolva https://github.com/dougmotshell/dougmotshell/actions/runs/31884406883

## Requisito refinado

- Objetivo: fazer o workflow `Generate Datas` (`.github/workflows/main.yml`) voltar a concluir
  com sucesso e a publicar a branch `output` (snake + troféus) sem quebrar o README.
- Fora de escopo: mudanças visuais do README (a seção de troféus segue com `<img>` simples, sem
  o `<picture>` claro/escuro do [ADR-0003](../../docs/adr/0003-light-dark-theme-parity.md) —
  registrado como pendência separada).

## Diagnóstico (causa raiz)

O step `Generate trophy SVG` falha com `exit code 3` desde **2026-07-22** — todas as execuções
agendadas do `Generate Datas` estão vermelhas desde então, e a branch `output` está congelada
nessa data (o snake também parou de atualizar, porque o deploy vem depois do step que falha).

Log do run 31884406883:

```
Error fetching user info for username: dougmotshell
Failed to fetch user info. Check token, username and rate limits.
##[error]Process completed with exit code 3.
```

A mensagem sugere token/username/rate limit, mas a causa é outra. Prova coletada com um workflow
temporário de diagnóstico rodando a `queryUserAll` da action com o `secrets.GITHUB_TOKEN`
(run 31902919951):

```json
"repositories": { "totalCount": 184, "nodes": [null, null, null, ...] },
"errors": [
  { "type": "FORBIDDEN",
    "path": ["user","repositories","nodes",0,"stargazers"],
    "message": "Resource not accessible by integration" }
]
```

O `secrets.GITHUB_TOKEN` é um *installation token* com escopo limitado ao repositório onde a
Action roda. Ele lê `contributionsCollection`, `followers`, `issues` e `pullRequests` do usuário
sem problema, mas **não consegue ler `stargazers` de outros repositórios** do Douglas. Como
`stargazers` é não-nulável no schema GraphQL, o GitHub anula o *node* inteiro e devolve
`nodes: [null, ...]`. A action então faz `nodes.reduce((acc, node) => acc + node.stargazers...)`,
estoura `TypeError` em `node` nulo, cai no `catch` de `requestUserInfo` (daí a mensagem genérica)
e sai com código 3.

Conclusão: **não há como gerar os troféus com o `GITHUB_TOKEN` padrão** — é necessário um PAT.
O README da action ([Erik-Donath/github-profile-trophy@feature/generate-svg](https://github.com/Erik-Donath/github-profile-trophy/tree/feature/generate-svg))
documenta `secrets.GITHUB_TOKEN`, o que é incorreto para perfis com mais de um repositório.

## Correção aplicada

1. Token do step passa a ser `${{ secrets.TROPHY_TOKEN || secrets.GITHUB_TOKEN }}` — usa o PAT
   quando o segredo existir, sem quebrar quem clonar o repo sem ele.
2. `continue-on-error: true` no step de troféus: uma falha do gerador não derruba mais o
   pipeline inteiro nem impede a atualização do snake.
3. Novo step de fallback: quando a geração falha, baixa o `trophies.svg` já publicado na branch
   `output` para o `dist/` antes do deploy. Sem isso, o `ghaction-github-pages` republicaria a
   branch sem o arquivo e a imagem do README quebraria (`build_dir` substitui o conteúdo todo).
   O step emite `::warning::` para a falha continuar visível na aba Actions.
4. `permissions: contents: write` explícito no job (o deploy escreve na branch `output`).

## Ação pendente do Douglas (fora do alcance do agente)

Criar o segredo `TROPHY_TOKEN` no repositório com um PAT **classic** com escopos `public_repo` e
`read:user`. Sem ele o pipeline fica verde e o perfil continua exibindo os troféus antigos
(gerados em 2026-07-22), mas os troféus deixam de ser atualizados.

```
gh secret set TROPHY_TOKEN --repo dougmotshell/dougmotshell
```

## Critérios de aceite

- [x] 1. Causa raiz identificada com evidência reproduzível (não suposição).
- [x] 2. `Generate Datas` conclui com sucesso mesmo sem o `TROPHY_TOKEN`.
- [x] 3. Branch `output` volta a ser publicada com os três arquivos (snake claro, snake escuro, troféus).
- [x] 4. Nenhuma imagem do README quebra durante ou após a correção.
- [x] 5. Workflow temporário de diagnóstico removido do repositório.
- [ ] 6. Com `TROPHY_TOKEN` configurado, os troféus voltam a ser gerados a cada execução (depende do Douglas).

## Referências

- SPEC: [SPEC-001](../../docs/specs/spec-profile-readme.md) · ADRs: [0004](../../docs/adr/0004-zero-cost-external-services.md)
- Arquivos-alvo: `.github/workflows/main.yml`
- Runs: [31884406883](https://github.com/dougmotshell/dougmotshell/actions/runs/31884406883) (falha original), 31902919951 (diagnóstico)

## Resolução

- Commits: `0b74c32` (correção do workflow), `f1fb9e6` (QA), merge [PR #2](https://github.com/dougmotshell/dougmotshell/pull/2) em `ef2cead`.
- Evidência final: run [31903263793](https://github.com/dougmotshell/dougmotshell/actions/runs/31903263793)
  na branch `main` — verde em 20s, com o warning do fallback visível; branch `output` republicada
  em 2026-08-15 com os três arquivos (snake claro/escuro regenerados, `trophies.svg` preservado).
  Validação prévia no branch do ticket: run 31903035597.
- Docs atualizados: [ADR-0005](../../docs/adr/0005-resilient-output-branch-publishing.md) (publicação
  resiliente do `output`), [lessons L-001 e L-002](../../agents/memory/lessons.md),
  [contexto de automação](../../agents/memory/context/automation.md), `AGENTS.md` (segredos e estado atual).
- Pendência: criar o segredo `TROPHY_TOKEN` para voltar a gerar troféus novos (critério 6).
