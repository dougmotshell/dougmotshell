# TCK-0001: Atualizar o perfil com a experiência profissional real

- **status:** in-review
- **owner:** content-writer
- **created:** 2026-08-15 · **by:** Douglas
- **type:** content
- **size:** M

## Pedido original (verbatim)

> baseado nos conhecimentos sobre mim "Douglas Matos da Silva" avalie este repositorio
> https://github.com/dougmotshell/dougmotshell que é o meu overview https://github.com/dougmotshell
> no meu github pessoal e com base do que sabe sobre mim crie um pull request com informações
> mais completas e atualizadas

## Requisito refinado

- **Objetivo:** o README de perfil descreve hoje apenas os projetos pessoais. Falta a maior
  evidência profissional do Douglas — 6+ anos de carreira, sendo desde mar/2020 na Intelie
  construindo telemetria de perfuração em tempo real para Óleo & Gás (Java/Kotlin/Spring,
  streams de sensores, React/TypeScript) e engenharia aumentada por IA (RAG, MCP, agentes).
  Um recrutador que abre o perfil não consegue inferir nada disso. Este ticket traz a
  experiência real, corrige o papel declarado, o link do LinkedIn e o stack.
- **Fora de escopo:** identidade visual (o layout e os serviços de imagem permanecem como
  estão); a seção automática de linguagens; qualquer conteúdo do LinkedIn ou do site pessoal.

### Regras de honestidade aplicadas (herdadas do banco de evidências do titular)

1. **Nunca declarar nível de senioridade.** O enquadramento oficial em carteira é *Pleno*;
   declarar "III"/"Senior" publicamente seria alegar um nível que o registro não sustenta.
   O README usa a **função** — `Full Stack Developer` — que é verdadeira hoje e continuará
   verdadeira depois de uma promoção.
2. **Nada de dado interno.** Sem código de ticket, nome de cliente, nome de repositório
   privado da empresa ou número de entregas internas.
3. **Cloud/Kubernetes não é operação.** Vai para "Exploring", não para o bloco de infra —
   há exposição e cursos, não operação de produção.
4. **Nada sobre nível de inglês.** A escrita técnica em inglês do próprio perfil é a
   evidência; nenhuma alegação de fluência é feita.
5. **Java sai de "learning".** É stack de produção há anos — mantê-lo como estudo subvende
   o perfil.

## Critérios de aceite (verificáveis)

- [x] 1. O README informa empresa, domínio de atuação e tempo de carreira, sem nenhum dado interno.
- [x] 2. O papel declarado é `Full Stack Developer` — nenhuma menção a nível/senioridade.
- [x] 3. Stack do README bate com o stack comprovado (Java, Kotlin, Spring, event streaming,
       PostgreSQL, MongoDB, React/TS, JUnit/Mockito, Jest/Testing Library, Cypress, Playwright,
       GitHub Actions, Docker); cloud aparece apenas como "Exploring".
- [x] 4. Link do LinkedIn aponta para o perfil atual (`/in/dougmotshell`) e o site pessoal está
       linkado na seção Connect.
- [x] 5. Todo recurso visual novo tem variantes dark + light + fallback com `alt` (ADR-0003).
- [x] 6. Os marcadores `<!-- LANGUAGES-START -->` / `<!-- LANGUAGES-END -->` permanecem intactos
       e o conteúdo entre eles não foi editado à mão (ADR-0002).
- [x] 7. `docs/context/profile.md` (fonte de verdade) e a SPEC-001 refletem o novo conteúdo.

## Referências

- SPEC: [SPEC-001](../../docs/specs/spec-profile-readme.md) · ADRs: [0002](../../docs/adr/0002-auto-generated-language-badges.md), [0003](../../docs/adr/0003-light-dark-theme-parity.md), [0004](../../docs/adr/0004-zero-cost-external-services.md)
- Arquivos/seções-alvo: `README.md` (header, typing, About Me, nova seção Work, Featured
  Projects, Tech Stack, Connect), `docs/context/profile.md`, `docs/specs/spec-profile-readme.md`

## Resolução (preenchido ao fechar)

- Commits: `TCK-0001: refresh profile content with professional experience`
- Evidência final (preview/run): PR aberto para revisão do Douglas — pendente de merge.
- Docs atualizados: `docs/context/profile.md`, `docs/specs/spec-profile-readme.md`
