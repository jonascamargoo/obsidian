---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2026-02-24'
---

**Data:** 24/02/2026

**Tópico:** #FineTuning #LLMOps #RAG #MachineLearning #SystemArchitecture

---

## ⚙️ 1. O que é Fine-Tuning?

Enquanto o RAG apenas aumenta o prompt com contexto externo, o fine-tuning (ajuste fino) retreina um modelo de linguagem de prateleira para melhorar seu desempenho em um contexto específico. A ideia central é retreinar o modelo com seus próprios dados para atualizar os parâmetros internos dele.

### Supervised Fine-Tuning (SFT) e Instruction Tuning

- O processo é tipicamente feito através de Supervised Fine-Tuning (SFT), onde o modelo é retreinado usando um dataset rotulado do domínio para o qual está sendo adaptado.
    
- No _Instruction fine-tuning_, o dataset inclui instruções (geralmente um prompt ou pergunta) e a melhor resposta esperada, conhecida como _ground truth_.
    
- Para fazer o ajuste fino, você alimenta o modelo com as instruções de entrada e mede o quão próxima a saída está da resposta correta do seu dataset.
    
- Esses resultados são então usados para ajustar os parâmetros internos do modelo, alinhando-os melhor com a resposta correta.
    

---

## ⚖️ 2. O Trade-off da Especialização

O fine-tuning transforma um modelo generalista em um especialista. Se você perguntar a um modelo comum sobre dores nas articulações e erupções cutâneas, ele dará uma resposta genérica em um tom genérico, pois não foi especializado em dados médicos. Com o _instruction tuning_ usando dados médicos, ele responderá com mais precisão, detalhes e no estilo apropriado para a área da saúde.

### O Custo da Especialização

- O processo de fine-tuning otimiza o desempenho apenas no domínio alvo.
    
- Como resultado, os ajustes nos parâmetros internos podem levar a uma queda de desempenho em solicitações de outros domínios.
    
- Para a engenharia de sistemas agênticos, esse trade-off é excelente: você pode pegar um modelo pequeno e leve e fazer um fine-tuning pesado para que ele execute apenas uma única tarefa (como ser um roteador de banco de dados vetorial) de forma brilhante.

	![[Pasted image 20260224022630.png]]

---

## 📏 3. A Regra de Ouro: RAG ou Fine-Tuning?

Um erro comum na engenharia de IA é tentar usar o fine-tuning para ensinar fatos novos ao modelo. O fine-tuning geralmente **não é uma boa maneira de ensinar novas informações a um LLM**. A adaptação afeta mais o estilo, a estrutura e as palavras que o modelo usa, tendo um impacto muito menor sobre o que o modelo "sabe" factualmente.

A distinção de arquitetura (o consenso atual) é clara:

- **RAG (Retrieval-Augmented Generation):** É a melhor solução para **injeção de conhecimento**. Se o LLM precisa ter acesso a novas informações, injete-as no prompt para que o modelo as incorpore na resposta.
    
- **Fine-Tuning:** É a melhor solução para **adaptação de domínio**. Se você quer que o LLM se especialize em uma tarefa (como roteamento) ou adote um tom específico, faça o fine-tuning.
    
	![[Pasted image 20260224022826.png]]
---

## 🤝 4. Abordagem Complementar (O Melhor dos Dois Mundos)

Em vez de alternativas concorrentes, encare-os como ferramentas complementares.

- Você pode usar os dois em conjunto no seu pipeline.
    
- Um caso de uso poderoso é fazer o fine-tuning de um modelo especificamente para torná-lo melhor em incorporar as informações recuperadas em suas respostas finais (especializando-o no seu papel dentro do sistema RAG).
    

> [!TIP] **Dica Prática de Engenharia** O fine-tuning é complexo e custoso. Antes de treinar o seu próprio modelo, procure em repositórios online de modelos preexistentes; frequentemente, você pode encontrar um modelo que já passou por fine-tuning para a tarefa ou domínio que você precisa.