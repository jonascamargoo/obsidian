---
description: Cria (ou atualiza) uma nota a partir de um tema ou conteúdo, no lugar certo do PARA
argument-hint: [tema ou conteúdo da nota]
---

Transformar o que o usuário trouxe em uma nota bem-feita, seguindo o protocolo conversacional do `CLAUDE.md`. Formaliza o fluxo padrão do second brain.

**Entrada:** $ARGUMENTS

## Procedimento (os 5 passos)

1. **Localizar** — com Grep (nome e conteúdo), verificar se já existe nota sobre o tema.
   - Existindo, **atualizar** a nota existente em vez de criar duplicata.
   - Não existindo, seguir para criar.

2. **Criar** no lugar certo:
   - Decidir a pasta pela regra PARA — tem objetivo com fim? `Projetos/`; responsabilidade/área viva? `Areas/<área>/`; referência externa? `Recursos/`; concluído? `Arquivo/`. Na dúvida entre duas, perguntar.
   - Nome do arquivo = título, sem redundância no corpo (começar direto em `## seção`).
   - Frontmatter completo (`tipo`, `area`, `tags`, `criada` = data de hoje) no estilo das notas vizinhas; tags da taxonomia controlada.

3. **Enriquecer** — complementar o que o usuário ditou com conhecimento próprio (contexto, exemplos, pipeline, relações) até a nota ficar completa. Afirmações factuais verificáveis acrescentadas por você (números, datas, benchmarks) levam ressalva curta de validação.

4. **Conectar** — adicionar wikilinks para notas relacionadas existentes (conferir que existem por nome) e incluir a nota no `_MOC.md` da área, no grupo certo.

5. **Confirmar e commitar**:
   - Conferir que nenhum link quebrado novo surgiu.
   - `git add` com **caminho explícito** da nota e do MOC (nunca `git add -A`); commit em português (`Nota: <título> em <área>`).
   - Responder com o caminho da nota e os links criados.

## Regras

- Só linkar para notas que existem; link para nota inexistente só como marca deliberada de nota-a-criar.
- Respeitar idioma PT-BR e o estilo (seções `##`, negrito em conceitos, callouts para resumo/aviso).
- Se a entrada estiver vazia, pedir o tema antes de prosseguir.
