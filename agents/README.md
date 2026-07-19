# Agentes de IA do Projeto — Índice

> Definições **canônicas e agnósticas de ferramenta** dos agentes que trabalham neste repositório de perfil do GitHub. Cada arquivo segue o padrão de mercado: markdown com frontmatter YAML (`name`, `description`) + corpo com papel, responsabilidades e regras — legível por Claude Code (subagents), Copilot, Codex, Gemini, GPT ou qualquer orquestrador.
>
> **Claude Code:** `.claude/agents/` aponta para esta pasta (symlink) — os agentes ficam invocáveis nativamente. **Outras ferramentas:** carregue o arquivo do agente como system prompt/instructions da sessão.

## Como o sistema funciona (visão de 1 minuto)

1. O desenvolvedor (Douglas) cria um **ticket** com a skill `/ticket` → nasce `tickets/TCK-NNNN/` com `ticket.md` (pedido + critérios de aceite) e `log.md` (auditoria append-only).
2. O **tech-lead** recebe todo ticket: analisa, refina critérios se preciso, e faz **handoff** ao agente responsável.
3. Cada agente trabalha, **registra tudo no log** e faz handoff conforme o [protocolo](handoff-protocol.md) — implementação → **code-reviewer** → **qa-validator**. Reprovou? Volta ao agente anterior com defeitos listados (loop). Aprovou nos critérios de aceite? `done`. **A cadeia é automática**: handoff registrado = próximo agente executa na hora; o fluxo inteiro roda sem o Douglas invocar nada e só para em `done` ou `blocked: human-input`.
4. **Auditoria:** nenhuma ação sem registro no `log.md` do ticket; commits sempre referenciam o ticket (`TCK-NNNN:`); logs são append-only. O que é **generalizável** sai do log e vira memória permanente: lições em [`agents/memory/lessons.md`](memory/lessons.md) e contexto operacional por área em [`agents/memory/context/`](memory/context/).
5. **Observação e controle:** o Douglas acompanha os markdowns dos tickets (`tickets/TCK-NNNN-*/`) e toma as decisões humanas do protocolo diretamente no fluxo — criar ticket (`/ticket`), handoff (`/handoff`), reprovar e **parar** (entrada `STOP` no `log.md`).

## Agentes

| Agente | Área exclusiva | Recebe de | Entrega para |
|---|---|---|---|
| [tech-lead](tech-lead.md) | Triagem, orquestração, decisões técnicas, desbloqueio | Douglas (tickets), qualquer agente travado | Todos |
| [content-writer](content-writer.md) | Conteúdo textual do perfil: bio, About Me, projetos em destaque, tom, cópia em inglês | tech-lead | readme-designer ou code-reviewer |
| [readme-designer](readme-designer.md) | Estrutura visual do README: badges, animações, `<picture>` claro/escuro, layout, acessibilidade | tech-lead, content-writer | code-reviewer |
| [automation-engineer](automation-engineer.md) | `generate_languages.py`, GitHub Actions (`main.yml`, `update-languages.yml`), branch `output`, serviços externos | tech-lead | code-reviewer |
| [code-reviewer](code-reviewer.md) | Revisão (markdown, Python, YAML, links, paridade de temas, convenções) | devs | qa-validator ou devolve ao dev |
| [qa-validator](qa-validator.md) | Validação contra critérios de aceite: renderização do README, links, CI verde | code-reviewer | done ou devolve (loop) |
| [docs-writer](docs-writer.md) | Docs do repo (`docs/`), ADRs, changelog | qa-validator (pós-done), tech-lead | tech-lead |

## Regras globais (valem para todos os agentes)

1. **Log ou não aconteceu:** toda ação relevante → entrada no `log.md` do ticket (formato no [protocolo](handoff-protocol.md)). Append-only: nunca editar/apagar entradas anteriores.
2. **Escopo exclusivo:** agente não mexe na área de outro; se precisar, handoff.
3. **Critérios de aceite são a definição de pronto** — não a opinião do agente.
4. **Loop limitado:** 3 devoluções no mesmo par de agentes → escalar ao tech-lead; tech-lead travado → escalar ao Douglas (marcar `blocked: human-input`).
5. **Convenções do repo:** identificadores/arquivos/commits en-US; docs internos pt-BR; conteúdo do `README.md` em inglês; custo zero ([ADR-0004](../docs/adr/0004-zero-cost-external-services.md)); paridade de temas ([ADR-0003](../docs/adr/0003-light-dark-theme-parity.md)); marcadores de linguagens são contrato ([ADR-0002](../docs/adr/0002-auto-generated-language-badges.md)).
6. Commits: `TCK-NNNN: <descrição imperativa>`; um ticket pode ter N commits, mas nenhum commit sem ticket (exceto hotfix documentado a posteriori). Obs.: commits do bot de CI (`Atualiza lista de linguagens automaticamente`) são automáticos e ficam isentos.
7. **Handoff executa, não espera:** registrado o handoff, o próximo agente assume imediatamente no mesmo fluxo. O Douglas só é acionado em `done` (relatório) ou `blocked: human-input` (perguntas).
8. **Agente ocupado não enfileira — spawna:** todo agente pode invocar **subagentes** ([protocolo, seção Subagentes](handoff-protocol.md#subagentes-e-paralelismo)) — instância do próprio tipo (`<agente>#N`) para assumir ticket novo da sua área ou paralelizar subtarefas. Subagente herda todas as regras; área de outro agente continua sendo handoff.
9. **Memória persistente — o mesmo erro não se comete duas vezes:** antes de trabalhar, ler [`agents/memory/`](memory/README.md) (lições + contexto da área); ao resolver erro generalizável, registrar lição `L-NNN`; ao mudar o conhecimento operacional da área, atualizar o `context/<área>.md`. Repetir erro com lição registrada é defeito **bloqueante**.
