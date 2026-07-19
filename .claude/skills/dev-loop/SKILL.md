---
name: dev-loop
description: Executa o ciclo completo de um ticket — triagem → implementação → code review → validação de QA — com handoffs e logs a cada etapa, em loop até todos os critérios de aceite passarem (ou escalar ao Douglas). Use com "/dev-loop TCK-NNNN".
---

# Skill: /dev-loop

Orquestra os agentes de [agents/](../../../agents/README.md) sobre um ticket até `done`, `blocked` ou limite de loops.

> **Execução automática:** este ciclo é disparado automaticamente ao final do `/ticket` (pós-triagem) e pela continuação do `/handoff` — o Douglas não precisa invocá-lo. A invocação manual (`/dev-loop TCK-NNNN`) serve para **retomar** um ticket parado.

## Passos

1. Ler o ticket; se `new`, rodar a triagem do tech-lead primeiro. Em seguida, **carregar a memória persistente**: [lições](../../../agents/memory/lessons.md) e o contexto da área ([agents/memory/context/](../../../agents/memory/context/)) relevantes ao ticket — lição aplicável muda a abordagem e é citada no log.
2. **Loop principal** (cada etapa registra ACTION/HANDOFF no log via o formato do protocolo):
   a. **Implementação** — assumir (ou invocar como subagente) o agente responsável: [content-writer](../../../agents/content-writer.md) (texto), [readme-designer](../../../agents/readme-designer.md) (visual), [automation-engineer](../../../agents/automation-engineer.md) (script/CI); commits `TCK-NNNN:`.
   b. **Code review** — papel do [code-reviewer](../../../agents/code-reviewer.md) sobre o diff completo; REJECT numerado devolve ao passo (a).
   c. **Validação** — papel do [qa-validator](../../../agents/qa-validator.md): conferir de verdade (renderização nos dois temas via `/readme-check`, links, CI verde quando aplicável), checklist de critérios com evidência; REJECT devolve ao passo (a).
   d. Todos os critérios ✓ → status `done`; acionar [docs-writer](../../../agents/docs-writer.md) se a entrega muda o README/comportamento ou tomou decisão estrutural (ADR).
3. **Limites**: 3 REJECTs no mesmo par → parar e escalar (resumo do impasse + opções para o Douglas). Falta decisão do Douglas → `blocked: human-input` com perguntas objetivas.
4. **Relatório final ao Douglas**: o que foi entregue, commits, evidências da validação, o que ficou pendente (se algo), e link do log para auditoria.

## Regras

- Papéis distintos são exercidos de verdade: o "reviewer" critica o diff como terceiro; ideal usar subagentes separados quando a ferramenta permitir. Review/QA sempre de cadeia distinta da do autor.
- **Paralelismo**: tickets independentes podem rodar `/dev-loop` simultaneamente. Agente responsável ocupado spawna subagente (`<agente>#N`) — entrada `SPAWN` no log ([protocolo](../../../agents/handoff-protocol.md#subagentes-e-paralelismo)).
- Nunca marcar critério como atendido sem evidência (preview/screenshot para o visual, run URL para o CI).
- **Memória**: a ACTION que resolve um REJECT termina com `Lição: L-NNN` (registrada em [lessons.md](../../../agents/memory/lessons.md)) ou `Lição: n/a — erro pontual`; erro que já tem lição registrada é defeito bloqueante. Ao fechar o ticket, se o conhecimento operacional da área mudou, atualizar `agents/memory/context/<área>.md`.
