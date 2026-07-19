# Propostas — Novas versões do README a partir das referências

> Cruzamento entre o **README atual** e a doc de [inspiração de perfis](../references/profile-readme-inspiration.md). Cada proposta é uma **versão completa e alternativa** do `README.md`, aplicando técnicas concretas obtidas dos perfis de referência — respeitando as regras do repo (paridade de tema [ADR-0003](../adr/0003-light-dark-theme-parity.md), custo zero [ADR-0004](../adr/0004-zero-cost-external-services.md), marcadores de linguagens [ADR-0002](../adr/0002-auto-generated-language-badges.md), sem `style=`).
>
> **Nada aqui está aplicado ainda** — são rascunhos para escolher. Ao adotar um, abra um [ticket](../../tickets/README.md) (`/ticket`) e siga o fluxo de agentes ([readme-designer](../../agents/readme-designer.md) + [content-writer](../../agents/content-writer.md), automação com [automation-engineer](../../agents/automation-engineer.md)).

## As três versões

| Proposta | Pista | Inspirada em | Para quem |
|---|---|---|---|
| [Variante A — Signal-First](variant-a-signal-first.md) | Minimalista, auto-atualizável | `simonw`, `rednafi`, `tw93`, `lauragift21` | Recrutadores / leitura rápida |
| [Variante B — Branded & Cohesive](variant-b-branded-cohesive.md) | Rico, mas disciplinado e coeso | `orhun`, `anuraghazra`, `Spiderpig86` | Mostrar marca pessoal sem perder o "wow" |
| [Variante C — Dashboard & Automation](variant-c-dashboard-automation.md) | Data-heavy, métricas em destaque | `DenverCoder1`, `anmol098`, `simonw` | Provar atividade/consistência com dados |

## Matriz de cruzamento — seção do README × técnica da referência

| Seção atual | Situação hoje | Técnica da referência | Origem | Onde entra |
|---|---|---|---|---|
| Header (wave + typing) | Typing com 5 linhas genéricas ("Full Stack Developer", "Always learning") | **Headline + missão de 1 linha** (especialidade óbvia em <5 s) | rednafi, orhun | A, B |
| Profile views / followers | Contadores de vaidade | **Remover** (sinal fraco) ou manter discreto | rednafi | A remove · B/C mantêm |
| About Me (code block) | Bom, já em 2 colunas | Manter; adicionar **tabela "⚡ Currently"** (projeto · foco · status) | orhun ("current work") | B |
| Featured Projects | Cards com badges (já feito neste repo) | Manter; segmentar/priorizar | orhun (projetos por área) | A, B, C |
| — (novo) | Não existe | **Feed auto-atualizável** de últimos posts/repos via Action | simonw, tw93, tallguyjenks | A, B, C |
| — (novo) | Não existe | **Métricas WakaTime** (tempo por linguagem) com enquadramento honesto | anmol098 | C |
| — (novo) | Não existe | **Badge "Build README"** de status da Action | simonw | C |
| GitHub Stats / Streak / Trophies | Três blocos decorativos separados | **Consolidar em 1 grid** com hierarquia clara | DenverCoder1 | C junta · A enxuga |
| Snake | Decorativo | Manter (baixo custo, alto charme) ou cortar no minimalista | — | B/C mantêm · A corta |
| Tech Stack | Grade rotulada (já feito) | Manter; no minimalista, **stack como texto** (extensões/lista) | caneco, rednafi | A simplifica · B/C mantêm ícones |
| Connect | Grade 4×2 de badges | **CTA explícito** + reduzir a poucos canais no minimalista | lauragift21 | A reduz + CTA · B/C mantêm |
| Most Used Languages (auto) | Gerado por CI | **Não mexer** — invariante de marcadores | — (regra do repo) | todas mantêm |

## Princípios herdados das referências (valem para as 3)

1. **Clareza em <5 s** — headline diz a especialidade antes de qualquer widget.
2. **Coesão > quantidade** — um tema/paleta; cada elemento tem propósito.
3. **Automação > decoração** — o que se auto-atualiza passa senioridade (candidato a ticket).
4. **Uma pista por público** — não misturar "recruiter-friendly" com "showcase lúdico".

## Blocos novos que dependem de automação (honestidade)

As Variantes A/B/C referenciam blocos **auto-atualizáveis** (últimos posts/repos, WakaTime) que **ainda não existem** neste repo. Nos rascunhos eles estão marcados com `<!-- requer Action -->`. Adotá-los = ticket para o [automation-engineer](../../agents/automation-engineer.md) (ver [ADR-0004](../adr/0004-zero-cost-external-services.md): só ferramentas gratuitas — `blog-post-workflow`, `waka-readme-stats`, `github-activity-readme`).
