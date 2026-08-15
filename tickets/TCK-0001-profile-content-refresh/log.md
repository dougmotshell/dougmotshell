# Log — TCK-0001

> Trilha append-only. Correção = nova entrada `CORRECTION`, nunca edição de entrada anterior.

## 2026-08-15 · ACTION · tech-lead

Triagem. Pedido classificado como `content`, tamanho M. O README atual cobre bem os projetos
pessoais e a apresentação visual, mas **não menciona a carreira** — que é a evidência mais forte
do perfil. Diagnóstico da lacuna:

| # | Achado | Gravidade |
|---|---|---|
| 1 | Nenhuma seção de experiência profissional (6+ anos, Intelie desde 2020, O&G em tempo real) | alta |
| 2 | `role` genérico ("Software Engineer \| Software Developer \| Vibe Coder Fixer") não diz o que ele faz | alta |
| 3 | `learning: ["Java"]` — Java é stack de produção há anos; listar como estudo subvende o perfil | alta |
| 4 | Stack sem Kotlin, Spring Boot, PostgreSQL, event streaming, Playwright/Cypress, GitHub Actions | média |
| 5 | AWS/GCP no bloco de infra sugerem operação em produção — a evidência é exposição + cursos | média |
| 6 | Link do LinkedIn aponta para vanity antigo (`/in/devdouglasmatos`); o atual é `/in/dougmotshell` | média |
| 7 | Site pessoal ausente da seção Connect | baixa |
| 8 | Formação (BSc em Engenharia de Software, 2024) ausente | baixa |
| 9 | `mathematics-studies` — projeto público e ativo — fora dos Featured Projects | baixa |

Handoff para o content-writer com as cinco regras de honestidade registradas no `ticket.md`.

## 2026-08-15 · HANDOFF · tech-lead → content-writer

Escopo entregue: texto do README (inglês), `docs/context/profile.md` (pt-BR) e o registro na
SPEC-001. Visual e automação **não** entram neste ticket.

## 2026-08-15 · ACTION · content-writer

Aplicado:

- **Header wave / typing SVG:** subtítulo passa a nomear função, domínio e stack real.
- **About Me:** objeto `douglas` reescrito — função, empresa, tempo de carreira, foco por
  camada (backend / frontend / data / AI), testing, formação. `Java` sai de `learning`.
- **Nova seção `💼 Work`:** o que ele constrói na Intelie, em quatro blocos, sem nenhum dado
  interno (sem código de ticket, cliente ou repo privado).
- **Featured Projects:** entra `mathematics-studies` (público, ativo, PWA bilíngue), rotulado
  como em progresso — é o estágio real (bootstrap).
- **Tech Stack:** adicionados Kotlin, Spring Boot, PostgreSQL, event streaming, Playwright,
  Cypress, JUnit/Mockito, GitHub Actions; AWS/GCP/Kubernetes movidos para "Exploring".
- **Connect:** LinkedIn corrigido para `/in/dougmotshell`; site pessoal adicionado.

Todos os recursos visuais novos são badges estáticos do shields.io (serviço já em uso, gratuito
— ADR-0004), que renderizam igual nos dois temas; os elementos com `<picture>` mantêm as três
variantes exigidas pelo ADR-0003. Marcadores de linguagens intocados.

## 2026-08-15 · HANDOFF · content-writer → Douglas (revisão no PR)

Três pontos precisam de decisão do titular, registrados no corpo do PR e **não** alterados aqui:

1. **Telefone pessoal exposto** nos links de WhatsApp e Telegram (`+55 21 99464-2132`) — o
   perfil é público e indexado; mantido como está, decisão do titular.
2. **Vanity antigo do LinkedIn** — trocado para `/in/dougmotshell` conforme o registro de
   2026-08-09; confirmar que o antigo não é mais o ativo.
3. **`ligcentro`** (Next 16 + React 19, i18n, PostgreSQL, Playwright, Docker) está ativo e
   público, mas sem `description` nem README — ficou fora dos Featured Projects por falta de
   descrição confiável. Vale um ticket próprio.

## 2026-08-15 · CORRECTION · qa-validator

Validação de links (critério 3 da SPEC-001) encontrou um **defeito preexistente, não introduzido
por este ticket**: o domínio pessoal linkado no card *Personal Website* está morto.

```
douglasmatosdasilva.com.br  ->  NXDOMAIN   (dns.google, 2026-08-15)
douglasmatosdev.com         ->  NXDOMAIN
douglasmatosdasilva.vercel.app -> 200 OK   ("Home Page // Douglas Matos da Silva")
```

Registro expirado ou removido — o site em si está no ar, só o domínio não resolve. Correções
aplicadas nesta branch:

- README: o botão *Live* do card **Personal Website** e o ícone novo de site na seção **Connect**
  apontam para `https://douglasmatosdasilva.vercel.app`.
- `docs/context/profile.md`: aviso registrado, com instrução de reverter para o domínio próprio
  quando ele voltar.

Ação para o Douglas (fora do escopo deste ticket): renovar/reapontar o domínio. Enquanto isso, a
mesma URL morta está no campo **blog** do perfil GitHub e no LinkedIn.

Demais validações: 48 URLs novas/alteradas testadas — todas `200`, exceto o LinkedIn (`999`, bloqueio
anti-bot esperado, vale para o link antigo e o novo). Marcadores `LANGUAGES-*` com um único par e
conteúdo intocado. Tags HTML balanceadas (`table`/`tr`/`td`/`picture`/`div`/`a`/`p`). Todos os
recursos com `<picture>` têm as três variantes do ADR-0003 e `alt` descritivo.

**Veredito:** critérios de aceite 1–7 atendidos. Ticket segue `in-review` até o merge do PR —
quem fecha é o Douglas, aprovando o conteúdo sobre a própria carreira.
