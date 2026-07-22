---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2026-02-24'
---

**Data:** 24/02/2026

**Tópico:** #AgenticAI #SystemArchitecture #LLMOps #RAG #Microservices

---

## 🔄 A Mudança de Paradigma

A introdução de workflows agênticos é uma maneira poderosa de melhorar o desempenho do seu sistema RAG à medida que ele amadurece. A forma típica de usar um modelo de linguagem é simplesmente alimentá-lo com um prompt e ele cospe uma resposta.

Em um sistema agêntico, há duas mudanças principais nesse modelo:

- As tarefas são agora tratadas como uma série de etapas e decisões.
    
- Cada etapa pode ser concluída por uma chamada a um LLM diferente.
    
- Os LLMs recebem acesso a uma variedade maior de ferramentas, como um interpretador de código, um navegador web ou um banco de dados vetorial de informações para referência.
    

---

## 🏗️ Padrões de Arquitetura Agêntica

Você pode pensar no design de um sistema agêntico essencialmente como o desenho de um fluxograma. Cada LLM ainda recebe uma entrada de texto e gera uma saída de texto, mas o sistema é configurado para que cada LLM conclua apenas uma tarefa na jornada do prompt.
![[Pasted image 20260224014228.png]]
Existem quatro padrões comuns a considerar:

### Sequencial
![[Pasted image 20260224020455.png]]

### Condicional
![[Pasted image 20260224020603.png]]

### Iterativo
![[Pasted image 20260224020624.png]]

### Paralelo
![[Pasted image 20260224020650.png]]

| **Padrão**      | **Mecânica Principal**                                                                                                             | **Exemplo Prático**                                                                                                                                         |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sequencial**  | Move a saída de forma linear através de uma série de LLMs.                                                                         | Um prompt passa por um analisador de query, um reescritor de query e um gerador de citações. Cada LLM foca em uma etapa e pode se especializar nela.        |
| **Condicional** | Utiliza um LLM para decidir qual caminho, dentre vários, um prompt deve seguir.                                                    | Um LLM "Roteador" pequeno avalia o prompt para determinar se uma chamada ao banco de dados vetorial é realmente necessária ou se ele pode pular essa etapa. |
| **Iterativo**   | Funciona de forma similar ao condicional, mas roteia o prompt para um ponto anterior no sistema global, formando um loop.          | Um LLM avaliador analisa um rascunho de código gerado e fornece feedback repetidamente até julgar que a solução é adequada.                                 |
| **Paralelo**    | Um LLM orquestrador divide um prompt em tarefas distintas, as atribui a LLMs separados e um LLM sintetizador recombina o trabalho. | Dois LLMs diferentes resumem e avaliam artigos de pesquisa distintos simultaneamente, e o orquestrador combina as descobertas.                              |

---

## ⚙️ A Visão da Engenharia: Modularidade e Custos

Uma das maiores vantagens técnicas é que você não precisa usar o mesmo LLM para cada etapa do fluxo de trabalho. O uso de um workflow agêntico provoca uma importante mudança de mentalidade, onde os LLMs parecem menos com soluções independentes e mais com peças modulares.

- **Modelos Leves:** LLMs roteadores e avaliadores podem ser modelos leves, rápidos e baratos de executar, pois possuem uma tarefa única e relativamente simples.
    
- **Modelos Robustos:** Você pode usar um modelo maior e mais potente para gerar a resposta de rascunho principal.
    
- **Especialistas:** É possível escolher um modelo que seja especialista apenas na geração de citações para assumir essa etapa específica do pipeline.
    

> [!TIP] **Ferramentas de Implementação**
> 
> Para sistemas agênticos simples, você pode implementar a lógica do fluxo de trabalho desejado por conta própria. No entanto, à medida que as coisas ficam mais complicadas, há uma grande variedade de ferramentas, bibliotecas e plataformas projetadas para ajudar a construir e gerenciar um sistema agêntico.

## Exemplo

- **Desacoplamento:** O **LLM Gerador** foca apenas em escrever código (pode ser um modelo otimizado para _coding_, como o GPT-4o ou Claude 3.5 Sonnet).
    
- **Execução Segura:** O código não vai direto para o usuário; ele passa por uma **Ferramenta** (um ambiente isolado/sandbox) que tenta executá-lo.
    
- **O Loop de Feedback:** O **LLM Avaliador** (que pode ser um modelo menor e mais rápido) lê o erro que o interpretador gerou e decide: "Isso falhou na linha 10". Ele envia esse feedback de volta para o LLM Gerador, forçando-o a tentar novamente.
    
- **Condição de Saída:** O loop só quebra quando o Avaliador define que a solução está correta, garantindo alta qualidade na ponta final.

![[Pasted image 20260224013425.png]]