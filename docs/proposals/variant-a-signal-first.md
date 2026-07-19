# Variante A — Signal-First (minimalista + auto-atualizável)

> Rascunho completo de `README.md`. Pista **recruiter-friendly**: tipografia primeiro, decoração mínima, feeds que se auto-atualizam. **Não aplicado** — para adotar, abra um [ticket](../../tickets/README.md).

## O que foi obtido das referências

| Mudança | Origem | Racional |
|---|---|---|
| Header vira **headline + missão de 1 linha** (especialidade óbvia); typing reduzido | `rednafi`, `orhun` | Clareza em <5 s; nada de "Always learning" genérico |
| **Remove** profile-views/followers, trophies, streak, snake | `rednafi` | Corta sinais de vaidade e decoração; senioridade = espaço em branco |
| Mantém **1** card de stats (o mais informativo) | `anuraghazra` | Um dado ancora, o resto distrai |
| Novo bloco **🆕 Latest** (posts/repos recentes) auto-gerado | `simonw`, `tw93`, `tallguyjenks` | Perfil que se mantém sozinho parece sempre atual |
| **CTA** explícito de contato + 1 detalhe humano | `lauragift21` | Minimalista ≠ frio; convida à ação |
| Tech Stack como **texto enxuto** (sem parede de ícones) | `caneco`, `rednafi` | Comunica a stack rápido, sem ruído |

> ⚠️ O bloco **🆕 Latest** depende de uma GitHub Action (ex.: `gautamkrishnar/blog-post-workflow`) — marcado com `<!-- requer Action -->`. Adotar = ticket para o [automation-engineer](../../agents/automation-engineer.md).

## Rascunho do README

~~~~markdown
<div align="center">

<!-- Slim header wave — identidade sem excesso -->
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:16213e&height=140&section=header&text=Douglas%20Matos&fontSize=48&fontColor=58a6ff&animation=fadeIn&fontAlignY=42" />
  <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,100:cbd5e1&height=140&section=header&text=Douglas%20Matos&fontSize=48&fontColor=0f172a&animation=fadeIn&fontAlignY=42" />
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,100:cbd5e1&height=140&section=header&text=Douglas%20Matos&fontSize=48&fontColor=0f172a&animation=fadeIn&fontAlignY=42" alt="Douglas Matos" />
</picture>

### Software Engineer — I build **AI-powered products** end to end.

LLM integrations · agentic workflows · offline-first PWAs · from prototype to CI/CD.

</div>

---

Hi, I'm Douglas 👋 — a software engineer from Brazil 🇧🇷. I turn fuzzy ideas into shipped
products: I wire LLMs (vision + voice) into real workflows, build PWAs that work offline,
and apply the same engineering rigor (specs, ADRs, tests, CI/CD) whether I'm on a team or solo.

**📫 Open to collaboration and opportunities** — reach me on
[LinkedIn](https://www.linkedin.com/in/devdouglasmatos/) or [email](mailto:douglasmatosdev@gmail.com).

**Currently:** AI products · agentic workflows · PWAs &nbsp;·&nbsp; **Learning:** Java · AI/ML · MCP · AI Agents

---

### 🔭 Selected Work

- **📚 [Librosistemo](https://github.com/dougmotshell/librosistemo)** — book-lending system on Next.js + TS, Google Sheets API, full Jest suite with coverage.
- **🌐 [Personal Website](https://douglasmatosdasilva.com.br)** — bilingual portfolio & blog (Next.js, MDX). · [source](https://github.com/dougmotshell/douglasmatosdasilva)
- **📻 [Rio Radio Player](https://radio-rio-de-janeiro.vercel.app)** — lightweight in-browser radio streaming. · [source](https://github.com/dougmotshell/radio-rio-de-janeiro-player)
- **🖼️ [Social Image Downloader](https://github.com/dougmotshell/social-img-downloader)** — TypeScript tool to pull media from social links.

_Also building (private):_ **LAMAR** — AI inventory bot on Telegram (Groq Llama vision + Whisper voice → Google Sheets) · **Lernema** — spaced-repetition study PWA ([live](https://lernema.vercel.app)) · **SCreator** — multi-tenant SaaS spun off from LAMAR.

---

### 🆕 Latest

<!-- requer Action: gautamkrishnar/blog-post-workflow (posts) ou jasonrudolph/activity (repos) -->
<!-- BLOG-POST-LIST:START -->
- _Auto-updated by CI — latest posts / releases will appear here._
<!-- BLOG-POST-LIST:END -->

---

### 🛠️ Stack

**Daily:** TypeScript · React / Next.js · Node.js · Java · Python
**AI:** OpenAI · Groq (Llama) · MCP · AI Agents
**Infra:** Docker · AWS / GCP · Linux · GitHub Actions

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=github_dark&include_all_commits=true&count_private=true&hide_border=true&bg_color=0d1117&title_color=58a6ff&icon_color=58a6ff&text_color=8b949e" />
  <source media="(prefers-color-scheme: light)" srcset="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=default&include_all_commits=true&count_private=true&hide_border=true" />
  <img height="160em" src="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=default&include_all_commits=true&count_private=true&hide_border=true" alt="GitHub stats" />
</picture>

</div>

---

<div align="center">

### 🧠 Most Used Languages (by bytes)

<!-- LANGUAGES-START -->
<!-- gerado por generate_languages.py — não editar à mão (ADR-0002) -->
<!-- LANGUAGES-END -->

</div>
~~~~

## Trade-offs

- **Ganha:** leitura em segundos, ar de senioridade, manutenção baixa (feeds automáticos).
- **Perde:** o "wow" visual (wave grande, snake, troféus). Se o objetivo é impressionar por estética, veja a Variante B.
- **Requer:** 1 Action para o bloco Latest (senão, remover o bloco).
