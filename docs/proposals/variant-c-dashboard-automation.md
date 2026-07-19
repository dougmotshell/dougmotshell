# Variante C — Dashboard & Automation (data-heavy)

> Rascunho completo de `README.md`. Pista **data-forward**: métricas em destaque, seções auto-geradas, hierarquia estrita. Prova atividade e consistência com dados. **Não aplicado.**

## O que foi obtido das referências

| Mudança | Origem | Racional |
|---|---|---|
| **Hierarquia estrita**: banner → métricas → projetos → stats → skills → langs | `DenverCoder1` | Densidade só funciona com ordem rígida |
| Bloco **⏱️ Dev Metrics (WakaTime)** — tempo por linguagem, auto-gerado | `anmol098` | Dado honesto e vivo sobre como o tempo é gasto |
| **Nota de enquadramento honesto** sob as métricas | `anmol098` | "Reflete código hospedado, não skill" → credibilidade |
| **Badge "Build README"** de status da Action + nota de auto-atualização | `simonw` | Automação transparente passa senioridade |
| Linha de **quick-metric badges** no topo (repos, langs, foco) | `DenverCoder1` | Resumo escaneável antes dos cards grandes |

> ⚠️ Blocos WakaTime e o badge de build dependem de Actions (`anmol098/waka-readme-stats`, mais o workflow que reescreve o README). Marcados com `<!-- requer Action -->`. Sem elas, remover os blocos. WakaTime é **gratuito** ([ADR-0004](../adr/0004-zero-cost-external-services.md)).

## Rascunho do README

~~~~markdown
<div align="center">

<!-- Banner + status de automação (simonw) -->
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a1a2e,100:16213e&height=180&section=header&text=Douglas%20Matos&fontSize=54&fontColor=58a6ff&animation=fadeIn&fontAlignY=40" />
  <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,50:e2e8f0,100:cbd5e1&height=180&section=header&text=Douglas%20Matos&fontSize=54&fontColor=0f172a&animation=fadeIn&fontAlignY=40" />
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:f8fafc,50:e2e8f0,100:cbd5e1&height=180&section=header&text=Douglas%20Matos&fontSize=54&fontColor=0f172a&animation=fadeIn&fontAlignY=40" alt="Douglas Matos" />
</picture>

**Software Engineer** · AI-powered products, end to end

<!-- requer Action: badge de status do workflow que reescreve o README -->
[![Build README](https://github.com/dougmotshell/dougmotshell/actions/workflows/update-languages.yml/badge.svg)](https://github.com/dougmotshell/dougmotshell/actions)
![Profile Views](https://komarev.com/ghpvc/?username=dougmotshell&label=Views&color=58a6ff&style=flat-square)
![Focus](https://img.shields.io/badge/focus-AI%20%C2%B7%20PWAs%20%C2%B7%20agents-8957e5?style=flat-square)

</div>

---

<div align="center">

### 📊 At a Glance

<table>
  <tr>
    <td>
      <picture>
        <source media="(prefers-color-scheme: dark)"  srcset="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=github_dark&include_all_commits=true&count_private=true&hide_border=true&bg_color=0d1117&title_color=58a6ff&icon_color=58a6ff&text_color=8b949e" />
        <source media="(prefers-color-scheme: light)" srcset="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=default&include_all_commits=true&count_private=true&hide_border=true" />
        <img height="165em" src="https://github-readme-stats-sigma-five.vercel.app/api?username=dougmotshell&show_icons=true&theme=default&include_all_commits=true&count_private=true&hide_border=true" alt="GitHub stats" />
      </picture>
    </td>
    <td>
      <picture>
        <source media="(prefers-color-scheme: dark)"  srcset="https://streak-stats.demolab.com?user=dougmotshell&theme=github-dark-blue&hide_border=true&ring=58a6ff&fire=ff6b6b" />
        <source media="(prefers-color-scheme: light)" srcset="https://streak-stats.demolab.com?user=dougmotshell&theme=default&hide_border=true&ring=0969da&fire=fd7e14" />
        <img height="165em" src="https://streak-stats.demolab.com?user=dougmotshell&theme=default&hide_border=true&ring=0969da&fire=fd7e14" alt="GitHub streak" />
      </picture>
    </td>
  </tr>
</table>

</div>

---

### ⏱️ Dev Metrics (last 7 days)

<!-- requer Action: anmol098/waka-readme-stats -->
<!--START_SECTION:waka-->
```txt
TypeScript   ██████████░░░░░░░░   —
Java         ████████░░░░░░░░░░   —
Python       ████░░░░░░░░░░░░░░   —
```
<!--END_SECTION:waka-->

> ℹ️ These metrics reflect time spent in tracked editors on hosted code — not a measure of skill, just an honest snapshot of where the hours go.

---

<div align="center">

### 🔭 Featured Projects

</div>

<!-- (mantém os cards atuais: Featured + Also Building) -->

---

<div align="center">

### 📈 Contribution Activity

<!-- (mantém o activity graph atual, picture dark/light) -->

### 🐍 Contribution Snake

<!-- (mantém o snake atual, picture dark/light) -->

### 🛠️ Tech Stack & Tools

<!-- (mantém a grade rotulada atual) -->

### 🌐 Connect with me

<!-- (mantém a grade 4×2 atual) -->

### 🧠 Most Used Languages (by bytes)

<!-- LANGUAGES-START -->
<!-- gerado por generate_languages.py — não editar à mão (ADR-0002) -->
<!-- LANGUAGES-END -->

</div>
~~~~

## Trade-offs

- **Ganha:** prova consistência com **dados** (streak, WakaTime, build badge); ótimo para quem valoriza atividade.
- **Perde:** é o mais "pesado"; exige disciplina de hierarquia para não virar poluição.
- **Requer:** WakaTime configurado + Actions (`waka-readme-stats` e o workflow de build). Sem isso, cai para a Variante B.
- **Honestidade:** manter a nota de enquadramento — métricas sem contexto enganam.
