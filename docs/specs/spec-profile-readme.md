# SPEC-001: README de Perfil (overview do usuário no GitHub)

> Spec do entregável principal do repositório ([ADR-0001](../adr/0001-github-profile-readme-as-product.md)). Documento vivo.

- **Status:** ativo
- **Início:** 2026-07-19
- **Dono:** content-writer (texto) + readme-designer (visual) + automation-engineer (seção automática)

## 1. Objetivo (o "quê" e o "porquê")

O `README.md` renderizado em **https://github.com/dougmotshell** faz um visitante (recrutador, colega, dev) entender, em ~10 segundos, **quem é o Douglas, no que ele trabalha e onde encontrá-lo** — com uma apresentação visual limpa que renderiza bem nos dois temas do GitHub e se mantém atualizada sozinha.

**Por que importa:** é a primeira (e às vezes única) impressão do perfil profissional do Douglas no GitHub.

## 2. Escopo

- **Dentro:** todo o conteúdo e visual do `README.md`; a seção automática de linguagens; a coerência com os assets gerados na branch `output` (snake, troféus).
- **Fora:** o código dos projetos linkados (vivem em seus próprios repos); a identidade visual de outras plataformas (LinkedIn etc.).

## 3. Critérios de aceite (os "testes")

| # | Critério verificável | Status |
|---|---|---|
| 1 | Um visitante identifica nome, papel/stack e formas de contato sem rolar muito | ☑ |
| 2 | Toda imagem/animação renderiza corretamente em tema **claro e escuro** + fallback ([ADR-0003](../adr/0003-light-dark-theme-parity.md)) | ☑ |
| 3 | Toda imagem tem `alt`; nenhum link/URL quebrado (via [`/readme-check`](../../.claude/skills/readme-check/SKILL.md)) | ☑ |
| 4 | A seção de linguagens é gerada por CI entre marcadores e reflete os repos reais ([ADR-0002](../adr/0002-auto-generated-language-badges.md)) | ☑ |
| 5 | Nenhum serviço pago; actions de terceiros com versão fixada ([ADR-0004](../adr/0004-zero-cost-external-services.md)) | ☑ |
| 6 | Não estoura em tela estreita (mobile) | ☑ |

## 4. Estrutura / seções

Ordem de renderização: header wave → typing SVG → profile views/followers → **About Me** → **What I Build at Work** → **Featured Projects** → GitHub Stats → Streak → Trophies → **Tech Stack & Tools** → Contribution Activity → Snake → **Connect with me** → **Most Used Languages** (auto) → footer wave.

A seção **What I Build at Work** é a evidência profissional do perfil e está sujeita às **regras de honestidade** de [context/profile.md](../context/profile.md): sem nível de senioridade, sem dado interno da empresa, cloud/Kubernetes apenas como estudo.

Contrato da seção automática: tabela reescrita entre `<!-- LANGUAGES-START -->` e `<!-- LANGUAGES-END -->` por `generate_languages.py` — não editar à mão.

## 5. Restrições e decisões (ADRs aplicáveis)

[ADR-0001](../adr/0001-github-profile-readme-as-product.md) (README é o produto) · [ADR-0002](../adr/0002-auto-generated-language-badges.md) (linguagens por CI) · [ADR-0003](../adr/0003-light-dark-theme-parity.md) (paridade de temas) · [ADR-0004](../adr/0004-zero-cost-external-services.md) (custo zero).

## 6. Riscos e mitigações

| Risco | Mitigação |
|---|---|
| Serviço de imagem fora do ar → imagem quebrada no perfil | Monitorar; abrir ticket e trocar por substituto gratuito ([ADR-0004](../adr/0004-zero-cost-external-services.md)) |
| Marcadores de linguagens corrompidos → README quebra no run | Invariante de um único par; `/readme-check` confere antes de fechar ticket |
| Conteúdo desatualizado (cargo, projetos) | Fonte de verdade em [context/profile.md](../context/profile.md); content-writer confere a cada ticket |
| Recurso visual só num tema | code-reviewer trata variante única como defeito bloqueante |

## 7. Registro de decisões e retrospectivas

| Data | Observação | Mudança |
|---|---|---|
| 2026-07-19 | Spec criada junto com a infraestrutura de IA do repo | Estado inicial documentado a partir do README existente |
| 2026-08-15 | O README contava os projetos pessoais, mas não a carreira — um visitante não inferia 6+ anos de experiência nem o domínio de atuação ([TCK-0001](../../tickets/TCK-0001-profile-content-refresh/ticket.md)) | Nova seção **What I Build at Work**; About Me com função, domínio e formação; stack alinhado ao real (Kotlin, Spring Boot, PostgreSQL, event streaming, Playwright/Cypress); cloud movida para "Exploring"; LinkedIn e site pessoal corrigidos; **regras de honestidade** formalizadas em `context/profile.md` |
