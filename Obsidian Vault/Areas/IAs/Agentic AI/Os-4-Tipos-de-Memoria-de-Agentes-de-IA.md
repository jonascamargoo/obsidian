---
title: Os 4 Tipos de Memória de Agentes de IA
tags:
  - IA
  - agentes
  - memória
  - CoALA
  - LLM
  - arquitetura-cognitiva
created: 2026-05-26
source: Vídeo educacional
framework: CoALA (Cognitive Architectures for Language Agents)
---

# Os 4 Tipos de Memória de Agentes de IA

> [!info] Sobre o framework
> O vídeo explora os quatro tipos principais de memória que agentes de IA bem projetados precisam, baseando-se no framework **CoALA** (*Cognitive Architectures for Language Agents*), desenvolvido por uma equipe de pesquisa de **Princeton**.

## 🧠 Analogia com a memória humana

A memória humana opera em diferentes níveis, e agentes de IA precisam de algo análogo:

- **Memória de curto prazo** → o que está ativo no cérebro agora
- **Conhecimento factual** → fatos como "Python é uma linguagem interpretada"
- **Habilidades aprendidas** → escrever, programar, dirigir
- **Experiência pessoal** → lembranças de eventos vividos

---

## 1. 🧮 Memória de Trabalho (*Working Memory*)

É a **janela de contexto** do agente — tudo que ele consegue "ver" naquele momento.

**Conteúdo típico:**
- Conversa atual
- Instruções de sistema
- Arquivos e dados carregados no prompt

> [!tip] Analogia
> Funciona como a **RAM** de um computador: rápida e imediatamente acessível, mas **volátil** (some quando a sessão termina) e **limitada em tamanho**.

**Limitações:**
- Mesmo janelas de 1 milhão+ de tokens têm um teto
- Desempenho degrada quando informações ficam "enterradas" no meio do contexto

> [!warning] Importante
> Todo agente tem memória de trabalho — mas todo chatbot também tem. A pergunta é: **o que mais um sistema agêntico precisa?**

---

## 2. 📚 Memória Semântica

É a **base de conhecimento** do agente — fatos, regras, convenções e documentação.

**Implementação na prática:**

| Abordagem acadêmica | Abordagem em produção |
|---|---|
| Bancos de dados vetoriais | Arquivos Markdown (`.md`) |
| Grafos de conhecimento | Estrutura simples e legível |

> [!example] Exemplo: Claude Code
> Usa um arquivo `Claude.md` na raiz do projeto contendo:
> - Arquitetura do projeto
> - Convenções de código
> - Comandos de build
> - Frameworks utilizados
> - O que **não** fazer
>
> Esse arquivo é carregado no contexto no início de cada sessão.

> [!danger] Sem memória semântica
> O agente está fadado a **repetir os mesmos erros** indefinidamente, pois não tem conhecimento persistente para consultar.

---

## 3. 🛠️ Memória Procedural

É como o agente **sabe fazer as coisas**.

**Padrão aberto:** `agent skills` no formato `skill.md`

Uma skill é simplesmente uma **pasta com um arquivo Markdown** descrevendo:
- O que a habilidade faz
- Instruções passo a passo
- Recursos relacionados (templates, scripts, arquivos)

**Exemplos de skills:**
- Criar uma apresentação de PowerPoint
- Executar uma revisão estruturada de código
- Gerar relatórios padronizados

### 🎯 Divulgação progressiva (*progressive disclosure*)

> [!tip] Conceito-chave
> O agente **não carrega todas as skills no contexto** de uma vez — isso estouraria o orçamento da memória de trabalho.

**Fluxo de carregamento:**

```
1. Agente vê apenas um índice leve
   └─ Nome + descrição (~100 tokens por skill)

2. Tarefa corresponde a uma skill
   └─ Instruções completas são carregadas

3. Execução em andamento
   └─ Recursos adicionais (arquivos, templates) entram conforme necessário
```

> [!note] Diferença em relação à memória semântica
> Na semântica, o conhecimento está **sempre presente** no contexto. Na procedural, ele é carregado **sob demanda**.

---

## 4. 📖 Memória Episódica

É o **registro de interações passadas**, decisões tomadas e lições aprendidas.

### Implementação ingênua vs. produção

❌ **Ingênua:** salvar todas as transcrições de conversa e buscar nelas

✅ **Produção:** **destilação** — o agente acumula notas para si mesmo, decidindo o que vale a pena lembrar

> [!example] Comparação prática
> **Transcrição bruta:** 45 minutos de sessão de debug
> **Memória destilada:** *"Da última vez que debugamos o módulo de autenticação, o problema estava na camada de middleware"*

> [!success] Onde mora o aprendizado
> É aqui que a memória começa a se parecer com **aprendizado genuíno** — o agente melhora ao longo do tempo.

### ⚠️ Desafios

> [!warning] O problema do esquecimento
> Memória episódica é o tipo **mais difícil** de implementar:
> - O que apagar?
> - Quando uma informação se torna obsoleta?
> - Se um usuário muda de emprego, manter ou descartar memórias antigas?
>
> Humanos esquecem naturalmente. Para agentes, **esquecer é um problema de engenharia**.

---

## 🎯 Nem todo agente precisa dos quatro tipos

A combinação necessária varia conforme a complexidade do agente:

| Tipo de agente | Trabalho | Semântica | Procedural | Episódica |
|---|:---:|:---:|:---:|:---:|
| Reflexo simples (termostato, roteador) | ✅ | ❌ | ❌ | ❌ |
| Suporte estreito (reset de senha) | ✅ | ❌ | ✅ | ❌ |
| Agente de programação | ✅ | ✅ | ✅ | ✅ |

---

## 💡 Conclusão

> [!quote] A diferença essencial
> A memória é exatamente o que **separa um chatbot de um agente**.
>
> Um chatbot apenas responde.
> Um agente entrega respostas **moldadas por conhecimento persistente e experiência acumulada**.

Um bom agente:
- Lembra do projeto
- Lembra das preferências do usuário
- Lembra dos erros — e **evita repeti-los**

---

## 🔗 Links relacionados

- [[Janela de Contexto]]
- [[RAG - Retrieval Augmented Generation]]
- [[Vector Databases]]
- [[Knowledge Graphs]]
- [[Claude Code]]
- [[Agent Skills]]
- [[Progressive Disclosure]]

## 📌 Tags

#IA #agentes #memória #CoALA #LLM #arquitetura-cognitiva #produtividade #desenvolvimento
