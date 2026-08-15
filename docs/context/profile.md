# Contexto — Douglas e o propósito do perfil

> **Fonte de verdade** para a cópia do perfil (usada principalmente pelo [content-writer](../../agents/content-writer.md)). Antes de escrever qualquer texto no `README.md`, confira aqui — afirmação desatualizada é defeito. Mantido em pt-BR (é doc interno); o texto do README em si vai em **inglês**.
>
> **Última revisão:** 2026-08-15 ([TCK-0001](../../tickets/TCK-0001-profile-content-refresh/ticket.md)).

## Quem é

- **Nome:** Douglas Matos da Silva
- **Usuário GitHub:** [`dougmotshell`](https://github.com/dougmotshell) — este repositório é o **overview do usuário** renderizado nessa página.
- **Pronomes:** He/Him
- **Localização:** Rio de Janeiro, Brasil 🇧🇷
- **Função:** **Full Stack Developer** na Intelie
- **Formação:** Bacharel em Engenharia de Software (Estácio, concluído em 2024, trabalhando em tempo integral)
- **Site pessoal:** portfólio bilíngue + blog técnico, servido hoje em https://douglasmatosdasilva.vercel.app
  - ⚠️ **Os domínios próprios estão fora do ar.** Em 2026-08-15, `douglasmatosdasilva.com.br` e `douglasmatosdev.com` respondem **NXDOMAIN** (confirmado no DNS público do Google) — registro expirado ou removido. Por isso o README aponta para o deploy da Vercel. Quando o domínio voltar, trocar de volta no README **e** aqui.
- **LinkedIn:** https://www.linkedin.com/in/dougmotshell (vanity atual — o antigo `devdouglasmatos` está aposentado)

## Carreira (o que o README precisa comunicar)

- Escreve software desde **2019** (freelance) e está na **Intelie desde março de 2020**.
- Time de **Performance KPIs para operações de Óleo & Gás**: telemetria de sondas de perfuração em tempo real — sensores, estados de sonda e KPIs operacionais que precisam estar certos e rápidos na tela de quem opera.
- **Backend:** Java e Kotlin com Spring — APIs REST com autorização por papéis, configuração por sonda, engines de classificação que rodam em tempo real **e** em reprocessamento histórico.
- **Dados e distribuídos:** microserviços sobre mensageria, PostgreSQL, MongoDB, exportação para BI/analytics. Casos reais de produção: correção de estouro de memória em pipeline de alto volume, falhas de integração entre serviços, análise de causa raiz de incidentes.
- **Frontend:** TypeScript/React — telas de configuração e integração front↔back com testes.
- **Qualidade:** JUnit e Mockito no backend; Jest, Testing Library, Cypress e Playwright no frontend — incluindo uma suíte E2E criada do zero, com cenários de borda de timezone e virada de meia-noite.
- **IA aplicada à engenharia:** base de conhecimento RAG do time por trás de um servidor MCP consultado por agentes, catálogo de padrões de IA, release notes geradas por IA no CI/CD.
- **Postura:** conduz features ponta a ponta (refinamento com especialistas de domínio → design de API → implementação → testes → documentação); decisor nominal em ADRs do time; revisor recorrente do código dos colegas.

## Regras de honestidade (obrigatórias — valem para todo texto público)

1. **Nunca declarar nível de senioridade** (III, Senior, Especialista…). O registro oficial em carteira é *Pleno*; o README declara a **função** (`Full Stack Developer`), que é verdadeira hoje e segue verdadeira depois de uma promoção.
2. **Nenhum dado interno da empresa:** sem código de ticket, nome de cliente, nome de repositório privado ou número de entregas internas. Descrever o **tipo** de trabalho, nunca o artefato interno.
3. **Cloud e Kubernetes = "Exploring"**, não infraestrutura de produção. Há cursos e serviços que ele desenvolve para rodarem em cloud; não há operação de infra em produção.
4. **Nada sobre nível de inglês.** O próprio README em inglês é a evidência disponível; nenhuma alegação de fluência.
5. **Java não é "learning"** — é stack de produção há anos.
6. **Frontend:** ele faz telas e integração front↔back; não reivindicar autoria de frontends que são de outra pessoa.

## No que trabalha / estuda (manter atualizado)

- **Trabalhando com:** telemetria em tempo real, backends Java/Kotlin+Spring, React/TypeScript, produtos com IA, workflows agênticos, PWAs.
- **Estudando:** Kubernetes, Azure/AWS/GCP, AI/ML.
- **Interesses:** algoritmos, clean code, UX/UI, open source.

## Projetos em destaque (Featured Projects do README)

| Projeto | Stack | Link |
|---|---|---|
| Mathematics Studies (em progresso) | Astro, TypeScript, KaTeX, PWA, conteúdo bilíngue | https://mathematics-studies.vercel.app · [source](https://github.com/dougmotshell/mathematics-studies) |
| Librosistemo | Next.js + TypeScript, Google Sheets API, Jest/Testing Library | https://github.com/dougmotshell/librosistemo |
| Personal Website | Next.js, MDX | https://douglasmatosdasilva.vercel.app · [source](https://github.com/dougmotshell/douglasmatosdasilva) — domínio próprio fora do ar, ver aviso acima |
| Rio de Janeiro Radio Player | Web player | https://radio-rio-de-janeiro.vercel.app · [source](https://github.com/dougmotshell/radio-rio-de-janeiro-player) |
| Social Image Downloader | TypeScript | [source](https://github.com/dougmotshell/social-img-downloader) — ⚠️ o deploy em `social-img-downloader.vercel.app` responde **404** (2026-08-15); por isso só o código está linkado no README |

- **Em construção (privado):** bots de Telegram com IA (visão + voz via Groq/Llama 4 Scout + Whisper e OpenAI, integrados a Google Sheets); PWAs de estudo offline-first movidos por workflows agênticos baseados em tickets, com CI/CD, CodeQL e Semgrep.
- **Fora do README por falta de descrição:** [`ligcentro`](https://github.com/dougmotshell/ligcentro) (Next 16, React 19, next-intl, PostgreSQL, Playwright, Docker) — público e ativo, mas sem `description` nem README próprio; entra quando houver descrição confiável.

## Propósito do perfil

Comunicar, em ~10 segundos e de forma honesta (sem hype), quem é o Douglas, no que trabalha e onde encontrá-lo — servindo também de **vitrine de como ele trabalha** (por isso o próprio repo usa spec, ADRs, C4 e fluxo de agentes). Detalhes de sucesso e critérios em [SPEC-001](../specs/spec-profile-readme.md).

## Tom de voz

- **Inglês**, direto e concreto; nada de superlativos vazios. O `funFact` ("I turn coffee into code") define o registro: leve, mas profissional.

> Ao mudar cargo, projetos ou stack, atualize este arquivo **e** o README no mesmo ticket.
