---
name: ticket
description: Cria um novo ticket de desenvolvimento no fluxo de agentes — coleta o pedido, gera tickets/TCK-NNNN-<slug>/ (ticket.md + log.md) a partir do template e entrega ao tech-lead para triagem. Use quando o Douglas pedir "/ticket <descrição>" ou quiser registrar uma tarefa.
---

# Skill: /ticket

Cria um ticket completo no padrão de [tickets/README.md](../../../tickets/README.md), para trabalhar neste repositório de perfil.

## Passos

1. **Número**: listar `tickets/TCK-*` e usar o próximo `NNNN` sequencial (começa em 0001). Reconferir `ls tickets/` imediatamente antes de criar (evita colisão entre sessões).
2. **Slug**: 2–4 palavras en-US derivadas do pedido (`TCK-0001-featured-projects-refresh`).
3. **Criar** `tickets/TCK-NNNN-<slug>/ticket.md` copiando `tickets/TICKET-TEMPLATE.md`:
   - Pedido original **verbatim** (nunca parafrasear na seção verbatim).
   - `type` (content|visual|automation|docs|bug), `size` e um rascunho de critérios de aceite se o pedido permitir inferir (marcar como "rascunho — validar na triagem").
4. **Criar** `tickets/TCK-NNNN-<slug>/log.md` com a primeira entrada:
   ```markdown
   ## [001] ACTION — <data hora> — /ticket
   - Ação: ticket criado a partir do pedido do Douglas
   - Resultado: ok — status new, owner tech-lead
   ```
5. **Handoff imediato**: assumir o papel do [tech-lead](../../../agents/tech-lead.md) (ou invocá-lo como subagente) para a triagem: classificar, dimensionar, validar/escrever critérios de aceite e registrar o HANDOFF `new → triaged` no log, no formato do [handoff-protocol](../../../agents/handoff-protocol.md).
6. **Continuar automaticamente**: a triagem NÃO encerra o fluxo. Se o ticket saiu `triaged`, entrar direto no ciclo do [/dev-loop](../dev-loop/SKILL.md) (conteúdo/visual/automação → review → QA) no mesmo fluxo, sem esperar novo comando. Só parar se a triagem resultou em `blocked: human-input` (listar as perguntas) ou se o pedido contradiz um ADR e precisa de decisão do Douglas.
7. **Responder ao Douglas ao final**: número do ticket, critérios, o que cada agente entregou e evidências — ou, se parou em `blocked`, as perguntas objetivas que destravam.

## Regras

- Um pedido com múltiplas entregas independentes = múltiplos tickets (avisar o Douglas) — e eles podem correr **em paralelo**: agente responsável ocupado spawna subagente (`<agente>#N`), conforme o [protocolo](../../../agents/handoff-protocol.md#subagentes-e-paralelismo).
- Nunca pular o log — a skill é a origem da trilha de auditoria.
- Na triagem (passo 5), o tech-lead consulta [agents/memory/](../../../agents/memory/README.md) e aponta no handoff as lições/contexto relevantes ao ticket.
- Convenções: pastas/slug en-US; conteúdo dos docs pt-BR; conteúdo do README em inglês.
