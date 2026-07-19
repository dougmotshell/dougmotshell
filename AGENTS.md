# AGENTS.md — Guia para Agentes de IA

> Arquivo canônico de instruções para agentes (Codex, GPT, Claude, Gemini, Copilot e outros).
> `CLAUDE.md`, `GEMINI.md` e `.github/copilot-instructions.md` apontam para cá — edite **somente este arquivo**.

## O que é este repositório

Repositório de **perfil do GitHub** de **Douglas Matos da Silva** (`dougmotshell/dougmotshell`) — o repositório especial (mesmo nome do usuário) cujo `README.md` é renderizado como **overview/vitrine do usuário** na página de perfil: **https://github.com/dougmotshell**. É a primeira coisa que qualquer visitante vê ao abrir o perfil do Douglas no GitHub. O **produto é o próprio README**: header animado, bio, projetos em destaque, stats, troféus, tech stack, grafo de contribuição, animação "snake" e uma tabela de linguagens **gerada automaticamente**.

Este projeto é mantido com metodologias de engenharia de software (C4, ADRs, spec-driven, fluxo de agentes com tickets) — não porque um perfil precise disso, mas porque o repositório também é uma **vitrine de como o Douglas trabalha**. A infraestrutura de IA aqui é a mesma linhagem do projeto `lernema`, adaptada para um repositório de perfil.

## Idioma e convenções

- **Conteúdo do `README.md`** (o perfil público): permanece no idioma atual — **inglês**, pois a audiência é global. Não traduzir para pt-BR sem pedido explícito do Douglas.
- **Documentação interna** (`docs/`, `agents/`, `tickets/`, comentários de código): **português brasileiro**. Termos técnicos consagrados em inglês podem aparecer no original.
- **Nomes de arquivos, pastas, variáveis, funções, branches, tags e commits em inglês en-US** — sempre. Ao criar qualquer arquivo novo, siga esta convenção.
- Datas no formato `AAAA-MM-DD`.
- **Custo financeiro zero** ([ADR-0004](docs/adr/0004-zero-cost-external-services.md)): todos os serviços usados (shields.io, capsule-render, readme-typing-svg, github-readme-stats, snk, github-profile-trophy) são gratuitos. Nunca introduzir serviço pago.

## Mapa do repositório

| Caminho | Conteúdo | Quando consultar |
|---|---|---|
| `README.md` | O perfil público (o produto). Contém marcadores gerados por CI | Antes de qualquer mudança visual/textual do perfil |
| `generate_languages.py` | Script que agrega linguagens de todos os repos e reescreve a tabela entre `<!-- LANGUAGES-START -->` e `<!-- LANGUAGES-END -->` | Ao mexer na seção de linguagens ou no CI de atualização |
| `.github/workflows/` | `main.yml` (snake + troféus → branch `output`) e `update-languages.yml` (roda o script Python, commita o README) | Ao mexer em automação/CI |
| `docs/architecture/c4-model.md` | Visão C4 deste repositório (perfil + automação + serviços externos) | Para entender a arquitetura geral |
| `docs/adr/` | Decisões de projeto (formato Nygard) | Antes de mudar uma decisão estrutural |
| `docs/specs/` | Specs por entregável (o README de perfil) | Ao criar/ajustar o perfil de forma estruturada |
| `docs/context/profile.md` | Contexto sobre o Douglas e o propósito do perfil | Antes de escrever bio/tom/conteúdo |
| `agents/` | Definições dos agentes de desenvolvimento (ver seção abaixo) | Ao trabalhar em qualquer tarefa via tickets |

## Regras para agentes

1. **Paridade de temas claro/escuro** ([ADR-0003](docs/adr/0003-light-dark-theme-parity.md)): toda imagem/animação no README usa `<picture>` com `prefers-color-scheme` para dark e light, mais um `<img>` de fallback. Adicionou um recurso visual novo? As duas variantes (+ fallback) são obrigatórias.
2. **Nunca quebrar a automação de linguagens**: os marcadores `<!-- LANGUAGES-START -->` / `<!-- LANGUAGES-END -->` são contrato entre o `README.md` e o `generate_languages.py`. Não removê-los, não editar o conteúdo entre eles à mão (o CI sobrescreve), não mudar o texto dos marcadores sem atualizar o script.
3. **Acessibilidade**: toda imagem tem `alt` descritivo; badges têm rótulo legível; contraste adequado nos dois temas.
4. **Serviços externos são gratuitos e substituíveis** (ADR-0004): ao adicionar um badge/gerador, preferir serviços consolidados e gratuitos; registrar o serviço e o motivo. Se um serviço morrer, propor substituto via ticket (não deixar imagem quebrada no perfil).
5. **Decisões estruturais viram ADR**: mudar o formato da seção de linguagens, trocar de serviço de stats, mudar a estratégia de deploy do `output` — tudo isso é um novo ADR (`docs/adr/`), nunca uma mudança silenciosa que contradiz um ADR existente.
6. **Novo entregável estruturado = nova spec**: copie `docs/specs/spec-template.md`. Hoje o entregável é o README de perfil (SPEC-001).
7. **Segredos**: o único segredo é o `GITHUB_TOKEN` das Actions — sempre via `secrets`/env, nunca hardcoded. O `generate_languages.py` lê `GITHUB_TOKEN` e `GITHUB_USERNAME` do ambiente.

## Estado atual

- **README de perfil ativo** com as seções: header wave, typing SVG, profile views/followers, About Me, Featured Projects, GitHub Stats, Streak, Trophies, Tech Stack, Contribution Activity, Snake, Connect, **Most Used Languages (auto)**, footer.
- **Automação diária** (cron `0 0,12 * * *` + `workflow_dispatch`): `update-languages.yml` regenera a tabela de linguagens; `main.yml` regenera snake + troféus na branch `output`.
- **Spec ativa**: [SPEC-001 — Perfil README](docs/specs/spec-profile-readme.md).
- **ADRs**: [0001](docs/adr/0001-github-profile-readme-as-product.md) (README como produto), [0002](docs/adr/0002-auto-generated-language-badges.md) (linguagens automáticas), [0003](docs/adr/0003-light-dark-theme-parity.md) (paridade de temas), [0004](docs/adr/0004-zero-cost-external-services.md) (custo zero).

## Sistema de agentes de desenvolvimento (`agents/` + `tickets/` + skills)

- **`agents/`** contém as definições canônicas de cada agente especializado (tech-lead, readme-designer, automation-engineer, content-writer, code-reviewer, qa-validator, docs-writer) — markdown com frontmatter, utilizável por qualquer ferramenta de IA. Claude Code: `.claude/agents` → symlink. Outras ferramentas: carregar o arquivo do agente como instructions da sessão.
- **Fluxo de trabalho**: todo desenvolvimento passa por tickets (`tickets/TCK-NNNN-*/`), com handoffs e loops de validação definidos em [`agents/handoff-protocol.md`](agents/handoff-protocol.md). **Auditoria é obrigatória**: toda ação de agente vira entrada append-only no `log.md` do ticket; commits usam prefixo `TCK-NNNN:`. Nenhum agente marca o próprio trabalho como validado — só o qa-validator fecha tickets, contra os critérios de aceite.
- **Skills disponíveis** (`.claude/skills/`): `/ticket` (criar ticket + triagem), `/handoff` (transição formal com log), `/dev-loop` (ciclo completo implementação→review→QA até done), `/readme-check` (validar o README: links, renderização, paridade de temas, marcadores).
- Agentes respeitam **escopo exclusivo** (não mexer na área de outro; handoff) e as regras globais de [`agents/README.md`](agents/README.md). Agente ocupado com um ticket **não enfileira** os novos da sua área: spawna **subagentes** (`<agente>#N`) para assumi-los ou paralelizar subtarefas — seção "Subagentes" de `agents/handoff-protocol.md`.
- **Memória persistente** (`agents/memory/`): sessões são efêmeras, o repositório lembra — [lessons.md](agents/memory/lessons.md) (lições `L-NNN`, append-only: erro → causa raiz → como evitar) e [context/](agents/memory/context/) (contexto operacional vivo por área). Todo agente **lê antes de trabalhar** e registra lição ao resolver erro generalizável.
