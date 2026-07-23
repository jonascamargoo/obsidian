# Second Brain — Vault Obsidian

Este repositório é um vault Obsidian (a raiz do repo = raiz do vault). Ele é o "second brain" do Jonas, operado de forma conversacional: o usuário compartilha conhecimento em conversa e o Claude cria, atualiza e organiza as notas.

## Estrutura (método PARA)

| Pasta       | Conteúdo                                                              |
| ----------- | --------------------------------------------------------------------- |
| `Inbox/`    | Captura rápida sem formato. Triar quando o usuário pedir.             |
| `Projetos/` | Esforços com objetivo e fim definidos (TCC, migrações, cursos ativos) |
| `Areas/`    | Áreas de conhecimento vivas (IAs, Infoblox, Produtos, ...)            |
| `Recursos/` | Referências, links, materiais de apoio sem área específica            |
| `Arquivo/`  | Concluídos. `Arquivo/Faculdade/` guarda as matérias da graduação      |

- Cada área tem um índice `_MOC.md` (Map of Content) que agrupa e comenta as notas da área. **Ao criar ou mover uma nota, atualize o `_MOC.md` da pasta.**
- `Home.md` na raiz é o dashboard de entrada (links para MOCs, projetos, Inbox).
- Imagens ficam na subpasta `imagens/` da própria área, referenciadas com `![[nome.png]]`.

## Convenções de notas

- **Idioma**: português brasileiro; termos técnicos consagrados podem ficar em inglês (em itálico na primeira ocorrência: _tool use_, _grounding_).
- **Título** = nome do arquivo, sem redundância dentro do corpo (começar direto em `## seção`).
- **Estilo**: seções `##`, listas com conceitos em **negrito**, callouts (`> [!info]`, `> [!warning]`) para resumos e avisos.
- **Wikilinks**: linkar conceitos que têm (ou merecem ter) nota própria com `[[Nome da Nota]]`. Link para nota inexistente é aceitável — marca uma nota a criar.

### Frontmatter (obrigatório em toda nota)

```yaml
---
tipo: conceito   # conceito | aula | projeto | referencia | moc
area: IAs        # nome da pasta de área/matéria (ou "sistema" para meta-notas)
tags:
  - ia/rag
criada: 2026-07-22
---
```

- Schema mínimo, não teto: notas de curso podem ter campos extras (`curso`, `aula`, `fonte`, `dificuldade`...).
- `criada`: data da criação real. Para notas antigas, a data do primeiro commit do arquivo.
- `tipo`:
  - `conceito` — nota atômica sobre um tema (a maioria)
  - `aula` — anotação de aula/curso, segue numeração `NN - Título.md`
  - `projeto` — planos, decisões e acompanhamento de um projeto
  - `referencia` — link ou material externo comentado
  - `moc` — índices (`_MOC.md`, `Home.md`)

### Tags

Minúsculas, kebab-case, hierarquia com `/`. Vocabulário raiz controlado — criar novas raízes só quando nenhuma servir:

- `ia/...` — ex.: `ia/rag`, `ia/agentes`, `ia/llmops`, `ia/prompt-engineering`
- `redes/...` — ex.: `redes/dns`, `redes/dhcp`
- `dev/...` — ex.: `dev/arquitetura`, `dev/testes`, `dev/design-patterns`
- `dados/...` — ex.: `dados/sql`, `dados/engenharia`
- `so`, `compiladores`, `algoritmos`, `matematica`, `produto`, `carreira`, `meta`

Tags classificam; não repetir no corpo da nota.

## Protocolo conversacional

Quando o usuário compartilhar conhecimento, pedir para anotar algo ou colar material:

1. **Localizar**: procurar (Grep por nome e conteúdo) se já existe nota sobre o tema. Existindo, **atualizar** em vez de duplicar.
2. **Criar** no lugar certo da estrutura PARA, com frontmatter completo e no estilo das notas vizinhas.
3. **Enriquecer**: a nota não se limita ao que o usuário ditou — complementar com conhecimento próprio (contexto, exemplos, pipeline, relações) até virar uma nota completa e autossuficiente. Afirmações factuais verificáveis que o Claude acrescentou (números, benchmarks, datas, nomes de produtos) levam uma ressalva curta de validação, pois a nota mistura o aprendizado do usuário com acréscimos do modelo.
4. **Conectar**: adicionar wikilinks para notas relacionadas existentes e atualizar o `_MOC.md` da área.
5. **Confirmar**: responder com o caminho da nota e os links criados.

Outras operações sob demanda: triar o `Inbox/`, arquivar projetos/áreas concluídos (mover para `Arquivo/` atualizando MOCs), revisar notas órfãs.

## Regras operacionais

- Nunca deletar nota sem confirmação explícita; preferir mover para `Arquivo/`.
- Renomeou/moveu nota? Verificar wikilinks que apontam para ela (`grep -r "[[Nome"`) e corrigir.
- Commits em português, mensagem curta descrevendo a mudança de conhecimento (ex.: "Nota: ReAct pattern em IAs/Agentic AI").
- Não editar `.obsidian/workspace.json` (estado de UI, muda sozinho).

### Git: nunca `git add -A` / `git add .`

Sempre adicionar **caminhos explícitos** dos arquivos que a sessão tocou (`git add "Caminho/Nota.md"`) e conferir `git status` antes de commitar. Motivo: o histórico de merge deste repo pode deixar deleções pendentes no working tree; um `git add -A` as efetiva sem aviso (já causou remoção indevida de notas em 2026-07). O usuário às vezes apaga/move notas direto no Obsidian — se algo aparecer como deletado e você não fez isso, **pergunte antes**, não recupere nem re-delete por conta própria.
