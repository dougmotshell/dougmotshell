# ADR-0002: Tabela de linguagens gerada por CI entre marcadores

- **Status:** aceito
- **Data:** 2026-07-19

## Contexto

A seção "Most Used Languages" deve refletir o uso real de linguagens nos repositórios do Douglas, por bytes, e manter-se atualizada sem trabalho manual. Editar à mão fica desatualizado e é tedioso; serviços prontos de "top languages" dão pouco controle sobre estilo (cores, logos, agregação, exclusão de forks).

## Decisão

Gerar a seção via um script Python próprio (`generate_languages.py`) rodado por GitHub Actions (`update-languages.yml`, cron diário + `workflow_dispatch`). O script agrega linguagens por bytes em todos os repositórios públicos (ignorando forks), monta uma `<table>` de badges (shields.io, cores/logos em `LANG_CONFIG`) e a reescreve **entre marcadores de contrato**:

```
<!-- LANGUAGES-START -->
... tabela gerada — NÃO editar à mão ...
<!-- LANGUAGES-END -->
```

Os marcadores são um contrato entre o `README.md` (readme-designer) e o script (automation-engineer): o script faz `content.split(START)[0] + tabela + content.split(END)[-1]`.

## Consequências

- ✅ Sempre atualizada, custo zero, com controle total de estilo.
- ✅ Separação limpa de responsabilidades via os marcadores.
- ⚠️ Marcador duplicado, removido ou renomeado **corrompe** o README no próximo run — regra dura: um único par, nunca editar o miolo à mão, nunca mudar o texto do marcador sem atualizar o script.
- ⚠️ Depende da API do GitHub e do `GITHUB_TOKEN`; linguagem sem entrada em `LANG_CONFIG` usa o estilo default (cinza).

## Alternativas rejeitadas

- **Editar a tabela manualmente** — desatualiza e dá retrabalho.
- **Serviço externo de "top languages" (imagem pronta)** — menos controle de estilo/agregação e mais uma dependência de terceiro na renderização.
