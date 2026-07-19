# Referências — Overview pages de perfil GitHub (inspiração de design)

> Doc de **referência** para o design visual do `README.md` deste perfil ([SPEC-001](../specs/spec-profile-readme.md), agente [readme-designer](../../agents/readme-designer.md)). Coletânea de perfis GitHub bonitos/impressionantes de vários usuários, com links, para servir de inspiração — **sem copiar**, respeitando as decisões do repo (paridade de tema [ADR-0003](../adr/0003-light-dark-theme-parity.md), custo zero [ADR-0004](../adr/0004-zero-cost-external-services.md)).
>
> Links verificados em 2026-07-19. Perfis que mostram o rodapé transitório "Something went wrong" do GitHub ainda renderizam o README completo — é fallback de UI, não link morto.

## Como usar esta doc

Escolha **uma pista** conforme o público-alvo — misturar dilui as duas:

- **Recruiter-friendly** → minimalista/tipografia + feeds auto-atualizáveis (`rednafi`, `lauragift21`, `simonw`, `tw93`).
- **Showcase/criativo** → animações e READMEs interativos via Actions (`timburgan`, `rossjrw`, `DenverCoder1`).

O perfil atual do `dougmotshell` fica no meio: rico/animado, mas profissional. As referências (a) e (b) são as mais aplicáveis.

---

## 1. Listas curadas / galerias

| Recurso | URL | O que oferece |
|---|---|---|
| **abhisheknaiidu/awesome-github-profile-readme** | https://github.com/abhisheknaiidu/awesome-github-profile-readme | A lista curada canônica. Perfis agrupados por estilo (GitHub Actions, Game Mode, Code Mode, Dynamic/Realtime, Minimalistic, Anime, Typing) + grande seção de geradores. Melhor ponto de partida. |
| **durgeshsamariya/awesome-github-profile-readme-templates** | https://github.com/durgeshsamariya/awesome-github-profile-readme-templates | ~5.3k★. Arquivos `.md` prontos para copiar + galeria: https://durgeshsamariya.github.io/awesome-github-profile-readme-templates/ |
| **coderjojo/creative-profile-readme** | https://github.com/coderjojo/creative-profile-readme | Centenas de perfis A–Z, cada um com screenshot. Arquivado (out/2023), mas ótimo para navegar por miniatura. |
| **maxontech/best-github-profile-readme** | https://github.com/maxontech/best-github-profile-readme | ~40 perfis "bonitos e únicos" selecionados a dedo, com preview. Site: https://maxrohowsky.github.io/best-github-profile-readme/ |
| **recodehive — Awesome GitHub Profiles** | https://recodehive.github.io/awesome-github-profiles/ | Galeria hospedada e pesquisável. |
| **GitHub Topics** | https://github.com/topics/beautiful-profile-readme · https://github.com/topics/profile-readme · https://github.com/topics/github-profile-readme | Feeds ao vivo, sempre atualizados (perfis auto-marcados). |
| **ReadmeDesign — 20 Best Examples of 2025** | https://readmedesign.com/blog-best-github-profile-readme-examples-2025 | Artigo conceitual: 5 arquétipos (Minimalist, Data Nerd, Creative Coder, Open Source Legend, Career Climber). |
| **DEV — 10 Standout GitHub Profile READMEs** | https://dev.to/github/10-standout-github-profile-readmes-h2o | Seleção editorial do próprio GitHub, mais criativa/interativa. |

---

## 2. Perfis individuais de destaque

### (a) Rico / animado — polido, porém decorado

| Perfil | Link | Por que se destaca / lição |
|---|---|---|
| **anuraghazra** | https://github.com/anuraghazra | Autor do `github-readme-stats`; perfil é a implementação de referência (header custom, card de stats tematizado, ícones de skill inline). **Lição:** auto-branding criativo funciona quando ancorado em credenciais reais + cards limpos. |
| **Spiderpig86** | https://github.com/Spiderpig86 | Seções modulares: shields sociais → quick facts → posts de blog auto-puxados → stack em SVG (devicon) → card de stats → 1 GIF. **Lição:** personalidade lê como charme, não amadorismo, quando a estrutura é disciplinada. |
| **orhun** | https://github.com/orhun | Marca "terminal/TUI" coesa: GIFs Ratatui dark+light, projetos segmentados por linguagem, tabela "current work", shields. **Lição:** um tema único e consistente vence uma pilha de widgets soltos. |

### (b) Clean / minimalista — tipografia primeiro, recruiter-friendly

| Perfil | Link | Por que se destaca / lição |
|---|---|---|
| **rednafi** | https://github.com/rednafi | Minimalismo quase puro: bio de uma linha, tabela de artigos recentes, **zero badges**. **Lição:** com escrita forte e output real, espaço em branco sinaliza senioridade. |
| **caneco** | https://github.com/caneco | Markdown simples, stack comunicada como extensões de arquivo (`.php`, `.js`); repos pinados carregam o peso visual. |
| **lauragift21** | https://github.com/lauragift21 | Minimalismo caloroso de dev-advocate: saudação, linha de links sociais, seções com divisórias, CTA de contato claro. **Lição:** minimalista ≠ frio — um detalhe humano + CTA torna memorável. |
| **tallguyjenks** | https://github.com/tallguyjenks | Estrutura limpa com divisórias `* * *`, ícones sociais pequenos, listas auto-alimentadas de YouTube/Medium/atividade. |
| **tw93** | https://github.com/tw93 | Ethos explícito ("qualquer adição dilui o resto"), feeds auto-atualizáveis de Releases/Posts, repos marcados por emoji. **Lição:** feeds automáticos mantêm o minimalismo vivo sem poluir. |

### (c) Dashboard / data-heavy — analytics em destaque

| Perfil | Link | Por que se destaca / lição |
|---|---|---|
| **DenverCoder1** | https://github.com/DenverCoder1 | Autor do `readme-typing-svg`; portfólio-dashboard completo (banner de digitação, streak, activity graph, achievements, 100+ badges). **Lição:** densidade só funciona com hierarquia estrita de seções. |
| **anmol098** | https://github.com/anmol098 | Autor do `waka-readme`; métricas WakaTime auto-geradas via Actions (tempo por linguagem, horário de commits). **Lição:** enquadramento honesto ("reflete código hospedado, não skill") gera credibilidade. |
| **simonw** | https://github.com/simonw | Padrão-ouro de perfil **auto-atualizável**: Actions reconstroem o README com releases, posts e TILs recentes + badge de build. **Lição:** automação > decoração — perfil que se mantém sozinho sempre parece atual. |

### (d) Criativo / não-convencional — interativo, lúdico

| Perfil | Link | Por que se destaca / lição |
|---|---|---|
| **timburgan** | https://github.com/timburgan | **Jogo de xadrez jogável** dentro do README: clique → Issue pré-preenchida → Actions parseiam → tabuleiro/leaderboard atualizam. **Lição:** o loop Issue → Actions → reescrita do README transforma página estática em app. |
| **rossjrw** | https://github.com/rossjrw | **Royal Game of Ur** multiplayer assíncrono: times, dados, tabuleiro SVG renderizado por Actions, log e stats. **Lição:** mesmo padrão do xadrez, levado além com estado em SVG rico. |
| **novatorem** | https://github.com/novatorem | Widget **Spotify now-playing** (Python + Vercel), amplamente forkado. |

---

## 3. Blocos de construção recorrentes (todos gratuitos — [ADR-0004](../adr/0004-zero-cost-external-services.md))

| Ferramenta | Uso | Já usada aqui? |
|---|---|---|
| [`github-readme-stats`](https://github.com/anuraghazra/github-readme-stats) | Cards de stats e top-langs (~65k★, o mais usado) | ✅ |
| [`readme-typing-svg`](https://github.com/DenverCoder1/readme-typing-svg) | Header de digitação animado | ✅ |
| [`capsule-render`](https://github.com/kyechan99/capsule-render) | Banners wave/gradiente | ✅ |
| [`github-profile-trophy`](https://github.com/ryo-ma/github-profile-trophy) | Troféus | ✅ |
| [`github-readme-streak-stats`](https://github.com/DenverCoder1/github-readme-streak-stats) | Streak de contribuições | ✅ |
| [`skillicons.dev`](https://skillicons.dev) / [Simple Icons](https://simpleicons.org) | Logos de tech | ✅ |
| [`github-readme-activity-graph`](https://github.com/Ashutosh00710/github-readme-activity-graph) | Gráfico de atividade | ✅ |
| [`Platane/snk`](https://github.com/Platane/snk) | Animação da cobrinha de contribuições | ✅ |
| [`waka-readme`](https://github.com/anmol098/waka-readme-stats) | Métricas de dev (WakaTime) via Actions | ⬜ candidato |
| Issue → Actions → reescrita do README | READMEs interativos/auto-atualizáveis | ⬜ candidato |

---

## 4. Lições transversais (aplicáveis ao nosso perfil)

- **Clareza em <5 s** — os melhores perfis deixam a especialidade óbvia de imediato (headline + missão de uma linha). *Já é critério na [SPEC-001](../specs/spec-profile-readme.md).*
- **Coesão > quantidade** — um tema/paleta consistente (terminal do orhun, contenção do tw93) supera parede de badges soltos.
- **Automação é o movimento profissional** — feeds auto-atualizáveis (simonw, tw93) e métricas (anmol098) mantêm o perfil fresco e passam senioridade. *Combina com a cultura de CI do repo — candidato a ticket futuro.*
- **Duas pistas claras** — recruiter-friendly (minimalista + feeds) vs. showcase (Actions interativas). Escolher uma por público.

## 5. Ideias de ticket derivadas destas referências

- Feed **auto-atualizável** de últimos posts/repos (padrão simonw/tw93) via Action — reforça a cultura de automação já presente no repo.
- Métricas **WakaTime** (`waka-readme`) com enquadramento honesto (padrão anmol098).
- Avaliar se o excesso de widgets decorativos está diluindo a mensagem (lição de coesão) — possível passe de simplificação.

> Ao agir sobre qualquer ideia acima, abra um [ticket](../../tickets/README.md) (`/ticket`) e siga o fluxo de agentes.
