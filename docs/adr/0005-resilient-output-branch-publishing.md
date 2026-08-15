# ADR-0005: Publicação resiliente da branch `output`

- **Status:** aceito
- **Data:** 2026-08-15

## Contexto

O workflow `Generate Datas` (`.github/workflows/main.yml`) monta um diretório `dist/` com três
artefatos — snake claro, snake escuro e `trophies.svg` — e o publica na branch `output` via
`crazy-max/ghaction-github-pages`. O README consome esses arquivos por URL `raw.githubusercontent`.

Duas propriedades desse arranjo se mostraram frágeis (TCK-0002):

1. **Um gerador que falha derruba todos os outros.** A geração de troféus quebrou em 2026-07-22 e,
   como o step ficava antes do deploy, o snake parou junto — congelado por três semanas sem que
   nada no perfil indicasse o problema.
2. **O deploy substitui a branch inteira.** `build_dir: dist` publica exatamente o que está em
   `dist/`. Um artefato ausente não fica desatualizado: ele **some** da branch `output`, e a
   imagem correspondente quebra no perfil público.

Some-se a isso o limite do `secrets.GITHUB_TOKEN`: é um *installation token* com escopo restrito
ao próprio repositório, incapaz de ler dados de outros repositórios do usuário (ver
[contexto de automação](../../agents/memory/context/automation.md)). Nem todo gerador consegue
funcionar apenas com ele.

## Decisão

A publicação da branch `output` é **resiliente por artefato**, com três regras:

1. Cada gerador de artefato roda com `continue-on-error: true` — a falha de um não impede os
   demais nem o deploy.
2. Todo gerador tolerante a falha tem um **step de fallback** que restaura o artefato já publicado
   na branch `output` para dentro do `dist/`. O deploy nunca publica um `dist` incompleto.
3. A falha continua **visível**: o fallback emite `::warning::` explicando o que falhou e o que
   fazer. Degradação graciosa não pode virar falha silenciosa.

Se o próprio fallback não conseguir recuperar o artefato, o job **falha** — deixando a branch
`output` intacta, o que preserva o perfil.

Segredos além do `GITHUB_TOKEN` são opcionais por design: o workflow lê `secrets.TROPHY_TOKEN ||
secrets.GITHUB_TOKEN`, de modo que um fork sem o segredo continue rodando (com troféus
degradados) em vez de quebrar.

## Consequências

- ✅ O perfil nunca exibe imagem quebrada por causa de um gerador com problema — no pior caso
  mostra o artefato da última execução bem-sucedida.
- ✅ Um gerador quebrado não bloqueia os outros; o snake atualiza mesmo com os troféus falhando.
- ✅ Fork sem segredos configurados continua funcional (custo zero, [ADR-0004](0004-zero-cost-external-services.md)).
- ⚠️ Um artefato pode ficar silenciosamente antigo se ninguém ler os warnings da aba Actions —
  a checagem periódica do CI passa a fazer parte da manutenção do perfil.
- ⚠️ O fallback depende de o artefato já existir na branch `output`; a primeira publicação de um
  artefato novo não tem rede de segurança.

## Alternativas rejeitadas

- **Manter o job falhando até alguém consertar** — foi o comportamento anterior: três semanas de
  CI vermelho, snake congelado e nenhuma ação. Falhar não protegeu nada.
- **Commitar os artefatos na `main`** em vez de publicar na `output` — polui o histórico do
  repositório com SVGs binariamente ruidosos a cada 12 horas.
- **Voltar a consumir o serviço hospedado de troféus** — foi justamente de onde se saiu
  (commit `fac9fd7`) por indisponibilidade; a geração local é mais previsível.
