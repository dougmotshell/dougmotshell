# Variante B — Branded & Cohesive (rico, porém disciplinado)

> Rascunho completo de `README.md`. Mantém o impacto visual do perfil atual, mas com **coesão de marca**: um tema ("engineer who ships AI products"), cada widget com propósito, e uma tabela de trabalho atual. **Não aplicado.**

## O que foi obtido das referências

| Mudança | Origem | Racional |
|---|---|---|
| **Tagline de marca** no header + typing focado em IA/produto (não genérico) | `orhun`, `anuraghazra` | Um tema consistente vence widgets soltos |
| Nova tabela **⚡ Currently** (projeto · foco · status) | `orhun` ("current work") | Diz no que está mexendo agora, com estado |
| Bloco modular **📰 Recent activity** auto-gerado | `Spiderpig86`, `tw93` | Seções modulares e feeds mantêm vivo |
| Stats/Streak agrupados sob **📊 By the numbers** (hierarquia) | `DenverCoder1` | Consolidar em vez de 3 blocos avulsos |
| Mantém snake + troféus (baixo custo, alto charme), mas **subordinados** | `Spiderpig86` (1 GIF, com propósito) | Personalidade sem virar bagunça |

> ⚠️ **📰 Recent activity** depende de Action (`jasonrudolph/build-your-own-readme` / `github-activity-readme`) — marcado com `<!-- requer Action -->`.

## Rascunho do README

~~~~markdown
<div align="center">

<!-- Header wave com tagline de marca -->
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a1a2e,100:16213e&height=200&section=header&text=Douglas%20Matos&fontSize=58&fontColor=58a6ff&animation=fadeIn&fontAlignY=36&desc=I%20ship%20AI-powered%20products%2C%20end%20to%20end&descAlignY=56&descColor=8b949e" />
  <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,50:e2e8f0,100:cbd5e1&height=200&section=header&text=Douglas%20Matos&fontSize=58&fontColor=0f172a&animation=fadeIn&fontAlignY=36&desc=I%20ship%20AI-powered%20products%2C%20end%20to%20end&descAlignY=56&descColor=475569" />
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,50:e2e8f0,100:cbd5e1&height=200&section=header&text=Douglas%20Matos&fontSize=58&fontColor=0f172a&animation=fadeIn&fontAlignY=36&desc=I%20ship%20AI-powered%20products%2C%20end%20to%20end&descAlignY=56&descColor=475569" alt="Douglas Matos — I ship AI-powered products, end to end" />
</picture>

<!-- Typing focado no tema (não genérico) -->
<a href="https://github.com/dougmotshell">
  <picture>
    <source media="(prefers-color-scheme: dark)"  srcset="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=58A6FF&center=true&vCenter=true&width=650&lines=Software+Engineer+%40+Brazil;LLM+integrations+%E2%80%94+vision+%2B+voice;Agentic+workflows+%26+offline-first+PWAs;Specs%2C+ADRs%2C+tests%2C+CI%2FCD" />
    <source media="(prefers-color-scheme: light)" srcset="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=0969DA&center=true&vCenter=true&width=650&lines=Software+Engineer+%40+Brazil;LLM+integrations+%E2%80%94+vision+%2B+voice;Agentic+workflows+%26+offline-first+PWAs;Specs%2C+ADRs%2C+tests%2C+CI%2FCD" />
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=0969DA&center=true&vCenter=true&width=650&lines=Software+Engineer+%40+Brazil;LLM+integrations+%E2%80%94+vision+%2B+voice;Agentic+workflows+%26+offline-first+PWAs;Specs%2C+ADRs%2C+tests%2C+CI%2FCD" alt="What I do" />
  </picture>
</a>

<p>
  <img src="https://komarev.com/ghpvc/?username=dougmotshell&label=Profile+Views&color=58a6ff&style=flat-square" alt="Profile views" />
  <img src="https://img.shields.io/github/followers/dougmotshell?label=Followers&style=flat-square&color=58a6ff" alt="Followers" />
</p>

</div>

---

### 🚀 About Me

<table>
<tr>
<td width="60%" valign="top">

```typescript
const douglas = {
  pronouns: "He/Him",
  location: "Brazil 🇧🇷",
  role: "Software Engineer — AI products, end to end",
  currently: {
    working: ["AI-powered products", "Agentic workflows", "PWAs"],
    learning: ["Java", "AI/ML", "MCP", "AI Agents"],
  },
  passions: ["Algorithms", "Clean Code", "UX/UI", "Open Source"],
  funFact: "I turn coffee ☕ into code",
};
```

</td>
<td width="40%" valign="middle" align="center">

<img alt="coding animation" width="100%" src="https://raw.githubusercontent.com/abhisheknaiidu/abhisheknaiidu/master/code.gif" />

</td>
</tr>
</table>

---

### ⚡ Currently

<table>
<tr><th align="left">Project</th><th align="left">Focus</th><th align="left">Status</th></tr>
<tr><td>🤖 <b>LAMAR</b></td><td>AI inventory bot — LLM vision + voice → Google Sheets</td><td>🟢 Active</td></tr>
<tr><td>📖 <b>Lernema</b></td><td>Offline-first study PWA with spaced repetition</td><td>🟢 Active</td></tr>
<tr><td>🏭 <b>SCreator</b></td><td>Multi-tenant SaaS spun off from LAMAR</td><td>🟡 In progress</td></tr>
<tr><td>📚 <b>Librosistemo</b></td><td>Book-lending system, full test coverage</td><td>🔵 Maintained</td></tr>
</table>

---

<div align="center">

### 🔭 Featured Projects

</div>

<!-- (mantém os cards atuais: Librosistemo, Personal Website, Rio Radio, Social Image Downloader,
     + Also Building: LAMAR / Lernema / SCreator / How I Build — sem alteração) -->

---

### 📰 Recent Activity

<!-- requer Action: jasonrudolph/build-your-own-readme ou github-activity-readme -->
<!-- START_SECTION:activity -->
- _Auto-updated by CI — recent commits, PRs and releases will appear here._
<!-- END_SECTION:activity -->

---

<div align="center">

### 📊 By the Numbers

<!-- Stats + top-langs lado a lado (mantém picture dark/light atual) -->
<table>
  <tr>
    <td><!-- github-readme-stats card (dark/light) --></td>
    <td><!-- top-langs compact card (dark/light) --></td>
  </tr>
</table>

<!-- Streak (mantém picture dark/light atual) -->

</div>

---

<div align="center">

### 🛠️ Tech Stack & Tools

<!-- (mantém a grade rotulada atual: Frontend / Backend & Infra / AI & ML / Tools) -->

### 🏆 Trophies · 🐍 Contributions

<!-- (troféus + snake mantidos, agrupados e subordinados ao conteúdo acima) -->

</div>

---

<div align="center">

### 🌐 Connect with me

<!-- (mantém a grade 4×2 atual de badges) -->

### 🧠 Most Used Languages (by bytes)

<!-- LANGUAGES-START -->
<!-- gerado por generate_languages.py — não editar à mão (ADR-0002) -->
<!-- LANGUAGES-END -->

</div>

<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="https://capsule-render.vercel.app/api?type=waving&color=0:16213e,50:1a1a2e,100:0d1117&height=120&section=footer" />
  <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&color=0:cbd5e1,50:e2e8f0,100:f8fafc&height=120&section=footer" />
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:cbd5e1,50:e2e8f0,100:f8fafc&height=120&section=footer" alt="Footer wave" />
</picture>
~~~~

> Os blocos com `<!-- (mantém ...) -->` reaproveitam o markup **já existente** no README atual (com paridade de tema) — resumidos aqui só para o rascunho não repetir 200 linhas.

## Trade-offs

- **Ganha:** impacto visual do atual **+** foco e coesão; a tabela ⚡ Currently comunica trabalho real.
- **Perde:** ainda é "pesado" — mais para portfólio/showcase do que para triagem de 5 s.
- **Requer:** 1 Action para Recent Activity (opcional).
