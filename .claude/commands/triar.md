---
description: Tria o Inbox — formata cada captura, adiciona frontmatter, conecta e arquiva no lugar certo
argument-hint: [vazio = todo o Inbox | nome de um item]
---

Processar capturas soltas do `Inbox/` e movê-las para o lugar certo do PARA, seguindo o `CLAUDE.md`.

**Alvo:** $ARGUMENTS  (vazio = triar todos os itens do Inbox)

## Procedimento

1. **Listar** os itens de `Inbox/`, **exceto** `_Sobre o Inbox.md` (morador permanente). Se vazio, informar e parar.
   - Se o argumento nomear um item, triar só esse.

2. Para **cada** item, entender o conteúdo e propor (sem aplicar ainda):
   - **Destino** pela regra PARA (`Projetos/` / `Areas/<área>/` / `Recursos/` / `Arquivo/`).
   - **Nome final** do arquivo (título limpo, sem redundância).
   - **Frontmatter** completo (`tipo`, `area`, `tags`, `criada`) inferido do conteúdo.
   - **Formatação**: estruturar em `## seções`, negrito nos conceitos, callout de resumo se couber — sem inventar conteúdo além do que o usuário capturou (enriquecer é opcional aqui; se enriquecer, marcar acréscimos factuais para validação).
   - **Wikilinks** para notas relacionadas existentes.

3. **Confirmar** o plano de triagem (pode ser item a item ou o lote). Se o usuário passou `aplicar`, pular a confirmação.

4. **Aplicar** (após ok), por item:
   - Criar a nota formatada no destino (com frontmatter e links) e remover o original do Inbox — usar `git mv` quando for essencialmente o mesmo arquivo renomeado/movido, ou criar+`git rm` quando reescrever bastante.
   - Atualizar o `_MOC.md` da área de destino.

5. **Fechar**: conferir links, `git add` com **caminhos explícitos** (nunca `git add -A`), commit em português (`Triagem: <n> itens do Inbox`), e resumir onde cada item foi parar.

## Regras

- O `Inbox/` deve terminar contendo **apenas** `_Sobre o Inbox.md`.
- Na dúvida sobre o destino de um item, perguntar em vez de chutar.
- Nunca descartar conteúdo do usuário; se algo não virar nota, perguntar o que fazer.
