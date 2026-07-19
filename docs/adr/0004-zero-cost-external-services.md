# ADR-0004: Somente serviços externos gratuitos

- **Status:** aceito
- **Data:** 2026-07-19

## Contexto

O perfil compõe vários recursos a partir de serviços de terceiros: shields.io (badges), capsule-render (waves), readme-typing-svg (typing), github-readme-stats/streak, Platane/snk (snake), github-profile-trophy (troféus). Esses serviços entram como imagens/URLs no README e como actions no CI. Não há orçamento para o perfil, e um perfil não deve depender de assinatura para renderizar.

## Decisão

Usar **exclusivamente serviços e actions gratuitos**. Ao adicionar um recurso, preferir serviços consolidados e gratuitos; registrar qual serviço e por quê. Actions de terceiros ficam com **versão fixada** (nunca `@main`). Se um serviço gratuito degradar ou sair do ar, abrir ticket e propor substituto — nunca deixar imagem quebrada no perfil nem introduzir um pago.

## Consequências

- ✅ Custo zero e reprodutível; qualquer pessoa pode dar fork sem barreira.
- ✅ Versões fixadas evitam que mudança silenciosa de terceiro quebre o perfil.
- ⚠️ Dependência de disponibilidade de terceiros: exige monitoramento (imagem quebrada = ticket) e substituibilidade em mente.
- Obrigação: todo serviço novo é auditado quanto a ser gratuito e estável antes de entrar.

## Alternativas rejeitadas

- **Serviços pagos/premium** para stats mais bonitos — fora de orçamento e desnecessário.
- **Self-hosting dos geradores** — sobre-engenharia para um perfil; contradiz o custo/esforço zero.
