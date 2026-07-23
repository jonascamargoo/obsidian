---
description: Revisão de saúde do vault — o que entrou, órfãs, MOCs e links a corrigir, com sugestões
argument-hint: [vazio = últimos 7 dias | Nd (ex. 30d) | YYYY-MM-DD]
---

Diagnóstico periódico da saúde do second brain e sugestão de manutenção. Leitura primeiro; só altera algo após o usuário escolher.

**Janela:** $ARGUMENTS  (vazio = últimos 7 dias)

## Coletar (somente leitura)

1. **Entrou na janela** — `git log --since` e/ou notas com `criada` recente: o que foi criado/alterado.
2. **Notas órfãs** — sem nenhum wikilink de entrada (excluir MOCs, `Home.md`, `_Sobre o Inbox.md`). Agrupar por pasta; separar Áreas ativas de `Arquivo/`.
3. **MOCs desatualizados** — para cada área, notas que existem na pasta mas **não** constam no `_MOC.md`.
4. **Links não-resolvidos** — wikilinks `[[...]]` cujo alvo não existe (distinguir notas-a-criar propositais de erros de digitação; imagens faltando à parte).
5. **Frontmatter** — notas sem frontmatter válido/completo (`tipo`, `area`, `tags`, `criada`).
6. **Inbox** — quantos itens aguardando triagem.

## Apresentar

Relatório curto e escaneável, por seção, com números e os itens mais relevantes (não despejar listas gigantes — resumir e mostrar exemplos). Terminar com **ações sugeridas**, ranqueadas por impacto, por exemplo:
- conectar as N órfãs de tal área (via `/conectar`);
- adicionar M notas faltantes aos MOCs;
- criar as notas-a-criar mais linkadas;
- triar o Inbox (via `/triar`);
- completar frontmatter faltante.

## Executar

Perguntar **quais** ações executar. Só então aplicar, uma de cada vez, com `git add` de **caminhos explícitos** (nunca `git add -A`) e commit em português por bloco de mudança. Se o usuário só quer o diagnóstico, parar após apresentar.

## Regras

- Não deletar nem mover nada sem confirmação explícita.
- Preferir reaproveitar as skills existentes (`/conectar`, `/triar`, `/nota`) em vez de reimplementar a lógica.
