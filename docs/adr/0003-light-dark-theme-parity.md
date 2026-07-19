# ADR-0003: Paridade de temas claro/escuro em toda imagem via `<picture>`

- **Status:** aceito
- **Data:** 2026-07-19

## Contexto

Visitantes do perfil usam o GitHub em tema claro **ou** escuro. Uma imagem/animação pensada só para fundo escuro (texto claro, transparência) fica ilegível no tema claro, e vice-versa. O GitHub não permite CSS nem detecção de tema por JS no README, mas **suporta** `<picture>` com `prefers-color-scheme`.

## Decisão

Todo recurso visual não-trivial do README (header/footer wave, typing SVG, stats, streak, activity graph, snake, etc.) é declarado com:

```html
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="...tema escuro..." />
  <source media="(prefers-color-scheme: light)" srcset="...tema claro..." />
  <img src="...fallback..." alt="descrição" />
</picture>
```

As duas variantes de tema **mais** um `<img>` de fallback são obrigatórias. Toda imagem tem `alt` descritivo.

## Consequências

- ✅ O perfil fica legível e coerente nos dois temas e em clientes que ignoram `prefers-color-scheme` (usam o fallback).
- ✅ Acessibilidade: `alt` em toda imagem.
- ⚠️ Mais markup por recurso; o code-reviewer trata "variante única / sem fallback / sem alt" como defeito bloqueante e o qa-validator valida a renderização **real** nos dois temas.

## Alternativas rejeitadas

- **Assumir só tema escuro** (comum em perfis) — quebra a legibilidade para quem usa tema claro.
- **Uma imagem "neutra"** — na prática não existe para waves/gradientes/SVG com texto; o resultado é sempre pior em um dos temas.
