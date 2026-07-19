# Memória persistente dos agentes

> Sessões de agente são efêmeras; **o repositório é a memória**. Esta pasta guarda o que sobrevive entre sessões: erros já cometidos (para nunca repeti-los) e o conhecimento operacional que torna qualquer agente efetivo desde o primeiro minuto. Regras completas na seção ["Memória persistente"](../handoff-protocol.md#memória-persistente-lições-e-contexto) do protocolo.

## O que tem aqui

| Arquivo | O que é | Disciplina |
|---|---|---|
| [`lessons.md`](lessons.md) | Lições aprendidas (`L-NNN`): erro → causa raiz → como evitar | **Append-only**; lição superada = nova lição referenciando a antiga |
| [`context/<área>.md`](context/) | Contexto operacional **vivo** por área: pegadinhas, estado atual, decisões em vigor | Editável, mas toda entrada leva data |

## Quem lê o quê (mapa agente → contexto)

| Contexto | Agentes |
|---|---|
| [`context/process.md`](context/process.md) | tech-lead, docs-writer, code-reviewer (+ todos, para o sistema de tickets) |
| [`context/readme.md`](context/readme.md) | content-writer, readme-designer |
| [`context/automation.md`](context/automation.md) | automation-engineer |
| [`context/qa.md`](context/qa.md) | qa-validator |

## Ciclo de uso (resumo)

1. **Antes de trabalhar**: ler o contexto da sua área + varrer `lessons.md` pela área/palavras-chave do ticket. Lição que mudou a abordagem → citar no log (`aplicada L-NNN`).
2. **Errou algo generalizável** (REJECT resolvido, CI quebrado por pegadinha, retrabalho por falta de contexto): registrar lição `L-NNN` — a ACTION que resolve o defeito termina com `Lição: L-NNN` ou `Lição: n/a — erro pontual` (justificado).
3. **Terminou um ticket que mudou o conhecimento da área** (novo serviço, novo comportamento de renderização, decisão operacional): atualizar o `context/<área>.md`, com data.
4. **Review/QA cobram**: repetir um erro que já tem lição registrada é defeito **bloqueante**; resolver REJECT sem a linha `Lição:` também.

## O que NÃO entra aqui

- Detalhe pontual de um ticket (fica no `log.md` do ticket).
- O que já está nos arquivos de agente, ADRs, specs ou READMEs (não duplicar — referenciar).
