# Documentação — Perfil GitHub `dougmotshell`

Este repositório é o **overview do usuário no GitHub** de Douglas Matos da Silva — o `README.md` renderizado em https://github.com/dougmotshell. A documentação aqui aplica ao próprio perfil as metodologias de engenharia de software que o Douglas usa no trabalho:

- **Modelo C4** — o perfil descrito em 4 níveis de zoom (contexto → contêineres → componentes → código/protocolos). Ver [architecture/c4-model.md](architecture/c4-model.md).
- **ADRs (Architecture Decision Records)** — cada decisão de projeto ("por que a tabela de linguagens é gerada por CI?", "por que paridade de temas?") registrada com contexto, decisão e consequências. Ver [adr/](adr/README.md).
- **Spec-Driven Development** — o entregável (o README de perfil) tem uma *spec* com objetivo, critérios de aceite e escopo, escrita antes de mexer. Ver [specs/](specs/spec-profile-readme.md).

## Mapa da documentação

| Documento | O que contém |
|---|---|
| [../AGENTS.md](../AGENTS.md) | Instruções canônicas para agentes de IA (Claude, Codex, Copilot, Gemini, GPT) |
| [../agents/README.md](../agents/README.md) | Squad de agentes, fluxo de tickets e regras globais |
| [architecture/c4-model.md](architecture/c4-model.md) | Modelo C4 do perfil (contexto, contêineres, componentes, protocolos) |
| [adr/README.md](adr/README.md) | Índice dos ADRs — decisões de projeto e suas justificativas |
| [specs/spec-profile-readme.md](specs/spec-profile-readme.md) | SPEC-001 — o README de perfil (objetivo, critérios, seções) |
| [specs/spec-template.md](specs/spec-template.md) | Template para novos entregáveis estruturados |
| [context/profile.md](context/profile.md) | Contexto sobre o Douglas e o propósito do perfil (fonte de verdade para a cópia) |
| [references/profile-readme-inspiration.md](references/profile-readme-inspiration.md) | Coletânea de overview pages de perfil GitHub bonitas (inspiração de design, com links) |
| [proposals/README.md](proposals/README.md) | Novas versões do README a partir das referências (3 variantes + matriz de cruzamento) |

## Como usar este repositório

1. Leia o [Modelo C4](architecture/c4-model.md) para entender o perfil como um sistema.
2. Leia os [ADRs](adr/README.md) para entender **por que** cada decisão foi tomada.
3. Ao trabalhar em qualquer mudança, abra um [ticket](../tickets/README.md) (`/ticket`) — o fluxo de agentes cuida do resto.
