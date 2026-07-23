---
description: Sugere e aplica wikilinks conectando uma nota às relacionadas do vault
argument-hint: [nome ou caminho da nota | vazio para listar órfãs]
---

Conectar uma nota ao resto do vault, seguindo as convenções do `CLAUDE.md`. Objetivo: reduzir notas órfãs criando wikilinks **certeiros** (poucos e bons, não muitos e fracos).

**Alvo:** $ARGUMENTS

## Procedimento

1. **Resolver o alvo**
   - Se o argumento nomear uma nota (título ou caminho), localize o arquivo com Glob/Grep. Havendo ambiguidade, liste as opções e pare para o usuário escolher.
   - Se o argumento estiver **vazio**: liste as notas órfãs (sem nenhum wikilink de entrada), agrupadas por pasta, e pergunte qual conectar. Não prossiga sem escolha.

2. **Entender a nota** — ler conteúdo e frontmatter (`area`, `tags`). Extrair os conceitos-chave.

3. **Levantar candidatas a relacionadas** — com Grep/Glob sobre o vault, **nunca inventando notas**:
   - Notas cujo **título aparece mencionado no corpo** do alvo → candidata a link inline forte.
   - Notas que **mencionam o título do alvo** no corpo delas → candidata a backlink recíproco.
   - Notas da **mesma `area`** com **tags em comum**.
   - Notas **irmãs na mesma pasta** e as listadas no `_MOC.md` da área.
   - Descartar a própria nota e as já linkadas por ela.

4. **Propor (sem editar ainda)** — listar as candidatas ranqueadas, cada uma com:
   - o caminho da nota,
   - por que é relacionada (1 linha),
   - a forma do link: **inline** (no ponto do texto onde o conceito aparece) ou seção **## Relacionadas** ao final (relação conceitual não mencionada no texto).
   Pedir confirmação. Se o usuário passou `aplicar` no argumento, pular a confirmação.

5. **Aplicar (após ok)**
   - **Inline**: envolver a primeira ocorrência do conceito no corpo com `[[...]]` (usar `[[Nota|texto exibido]]` quando diferirem). Nunca duplicar um link já existente.
   - **Relação não mencionada**: adicionar/atualizar uma seção `## Relacionadas` ao fim, com bullets de wikilinks comentados.
   - **Backlinks recíprocos**: quando fizer sentido, adicionar o link de volta na outra nota (confirmar quais).
   - **MOC**: se a nota não constar no `_MOC.md` da área, incluí-la no grupo certo.

6. **Verificar e fechar**
   - Conferir que nenhum link quebrado novo surgiu (todos os alvos resolvem por nome).
   - Commit em português: `Conectar: <nota> (N wikilinks)`.
   - Responder com resumo: links inline, backlinks recíprocos e se o MOC foi tocado.

## Regras

- Só linkar para notas que **existem** (conferir por nome). Link para nota inexistente só se o usuário pedir para marcar uma nota-a-criar.
- **Conectar ≠ reescrever**: não alterar o texto da nota além de inserir os wikilinks.
- Preferir 3–6 links fortes a uma enxurrada de links fracos.
