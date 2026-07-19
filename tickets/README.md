# Tickets — Fluxo de desenvolvimento

Todo trabalho neste repositório de perfil passa por um **ticket**: uma pasta `TCK-NNNN-<slug>/` com o pedido, os critérios de aceite e o log de auditoria append-only. O ciclo é orquestrado pelos [agentes](../agents/README.md) conforme o [handoff-protocol](../agents/handoff-protocol.md).

## Estrutura de um ticket

```
tickets/
  TCK-NNNN-<slug>/
    ticket.md   # pedido verbatim, critérios de aceite, referências, resolução
    log.md      # trilha append-only: ACTION / HANDOFF / REJECT / SPAWN / STOP / CORRECTION
```

## Como criar

Use a skill [`/ticket`](../.claude/skills/ticket/SKILL.md) — ela numera, cria a pasta a partir de [`TICKET-TEMPLATE.md`](TICKET-TEMPLATE.md), abre o `log.md` e entrega ao tech-lead para triagem (que segue automaticamente para o [`/dev-loop`](../.claude/skills/dev-loop/SKILL.md)).

## Convenções

- **Número** `NNNN` sequencial a partir de `0001`; **slug** en-US (`TCK-0001-featured-projects-refresh`).
- **`type`**: `content` | `visual` | `automation` | `docs` | `bug`.
- **Commits**: prefixo `TCK-NNNN:` (exceto o commit automático do bot de linguagens).
- **Log append-only**: correção = nova entrada `CORRECTION`, nunca edição de entrada anterior.
- Só o [qa-validator](../agents/qa-validator.md) fecha ticket (`done`), contra os critérios de aceite.
