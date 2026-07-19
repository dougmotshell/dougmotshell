---
name: readme-check
description: Valida o README de perfil — checa links quebrados, marcadores de linguagens, presença de fallback de tema em toda imagem e boa-formação do HTML/markdown. Use após mudanças no README ou antes de fechar um ticket visual. Substitui, neste repo, o papel de "documentação viva" do lernema.
---

# Skill: /readme-check

Verificação automatizável do `README.md` deste repositório de perfil. Papel executor: [qa-validator](../../../agents/qa-validator.md) (e o [readme-designer](../../../agents/readme-designer.md) roda antes de entregar). É a checagem que substitui, neste repo, o `/user-manual` (Playwright) do lernema — aqui não há telas de app para capturar; o "produto" é um único README renderizado pelo GitHub.

## O que checar (checklist)

1. **Marcadores de linguagens** ([ADR-0002](../../../docs/adr/0002-auto-generated-language-badges.md)): existe **exatamente um** `<!-- LANGUAGES-START -->` e **um** `<!-- LANGUAGES-END -->`, nessa ordem, com uma `<table>` bem-formada entre eles. Marcador duplicado/ausente quebra o `generate_languages.py`.
2. **Paridade de temas** ([ADR-0003](../../../docs/adr/0003-light-dark-theme-parity.md)): todo bloco `<picture>` tem `<source media="(prefers-color-scheme: dark)">`, `<source media="(prefers-color-scheme: light)">` e um `<img>` de fallback. Toda imagem tem `alt`.
3. **Links e imagens**: todas as URLs (badges, serviços, repos dos Featured Projects, redes sociais) resolvem — sem 404.
4. **HTML/markdown**: tags abertas/fechadas corretamente (`<picture>`, `<table>`, `<td>`, `<a>`); nenhum `style="..."` (o GitHub sanitiza — usar `align`).
5. **Renderização real**: conferir no preview do GitHub (ou renderizador fiel) nos dois temas — não confiar só no markdown-fonte.

## Passos sugeridos (custo zero, sem serviço externo)

```sh
# 1. Marcadores presentes e únicos
grep -c "LANGUAGES-START" README.md   # deve ser 1
grep -c "LANGUAGES-END"   README.md   # deve ser 1

# 2. Toda <picture> tem duas <source> e um <img> (inspeção)
grep -n "<picture>\|prefers-color-scheme\|<img" README.md

# 3. Imagens sem alt (deve retornar vazio)
grep -noE '<img[^>]*>' README.md | grep -v 'alt='

# 4. Coletar e testar links/URLs (checagem manual/curl das URLs encontradas)
grep -noE 'https?://[^")> ]+' README.md | sort -u
```

Para os links, testar cada URL única (ex.: `curl -sI <url>` esperando 2xx/3xx). Registrar no log do ticket a lista verificada e o resultado.

## Regras

- Verificação **sempre** contra a renderização real, não só o texto-fonte.
- Nunca editar o conteúdo entre os marcadores de linguagens à mão (o CI sobrescreve) — se a tabela estiver errada, o defeito é no `generate_languages.py` (handoff ao automation-engineer).
- Evidência obrigatória: a saída dos comandos + preview/screenshot dos dois temas entra no log do ticket ([qa-validator](../../../agents/qa-validator.md)).
