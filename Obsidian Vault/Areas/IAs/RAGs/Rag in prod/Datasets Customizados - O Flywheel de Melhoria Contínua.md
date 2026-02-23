**Data:** 23/02/2026 **Tópico:** #LLMOps #DataEngineering #RAG #Evaluation #RootCauseAnalysis

---

## 🎯 Por que construir Datasets Customizados?

O objetivo é triplo:

1. **Auditoria Histórica:** Entender profundamente como o sistema se comportou.
    
2. **Experimentos Offline:** Rodar novas versões do sistema (redesign) contra prompts reais do passado para prever performance em produção.
    
3. **Personalização:** Ajustar o sistema especificamente para o tipo de tráfego que ele realmente recebe.
    

---

## 🛠️ Modelagem de Dados: O que armazenar?

A estrutura de um dataset customizado deve ser reflexo do que você deseja avaliar. Para engenheiros, isso significa que a tabela de logs pode ter **dezenas de colunas**.

### 1. Nível de Sistema (End-to-End)

Essenciais para avaliar a experiência final do usuário.

- `user_query`: O prompt inicial bruto.
    
- `final_response`: A saída gerada pelo LLM.
    
- `customer_id`: Para filtrar comportamento por perfis de cliente.
    

### 2. Nível de Componente (Deep Inspection)

Cruciais para isolar falhas em pipelines complexos (Agentic Workflows).

- **Retriever:** Chunks retornados e seus scores de similaridade.
    
- **Re-ranker:** Ordem dos documentos antes e depois do processamento.
    
- **Query Rewriter:** A versão otimizada da query enviada ao Vector DB.
    
- **Router LLM:** A decisão tomada pelo roteador (ex: enviar para busca ou para geração de imagem).
    

---

## 🔍 Análise de Causa Raiz e Clustering

### Identificação de Gaps de Conhecimento

Ao filtrar logs por tópicos (ex: "reembolsos" vs "atrasos de produto"), você pode descobrir que o sistema falha em áreas específicas.

- **Diagnóstico:** Se perguntas sobre "atrasos" performam mal, os logs podem revelar que o **Retriever** não encontra documentos relevantes.
    
- **Solução:** Ingestão de novos dados na Base de Conhecimento.
    

### Detecção de Erros de Roteamento

Um sistema robusto de logs permite identificar falhas lógicas em fluxos multimodais.

> [!EXAMPLE] **Caso de Estudo: Diagramas Mermaid.js**
> 
> - **Problema:** Usuários reclamavam de gráficos de baixa qualidade.
>     
> - **Descoberta via Logs:** O **Router LLM** interpretava "desenhe um gráfico" como um pedido de imagem e enviava para um modelo _text-to-image_ (ruim em gráficos), em vez de enviar para o gerador de código Mermaid.js.
>     
> - **Correção:** Ajuste do _system prompt_ do roteador baseado nos logs de falha.
>     

### Visualização e Tendências

Uma técnica avançada é aplicar **algoritmos de clustering** nos prompts de entrada.

- Isso permite agrupar perguntas por "Tópicos de Alto Nível" (ex: Troubleshooting, Vendas, Billing).
    
- Você pode então rodar seu pipeline de avaliação (Evals) em clusters específicos para identificar onde o sistema está subperformando.
    

---

## 🎡 O Ciclo de Vida do Dataset

1. **Logging:** Captura extensiva em produção (Traces/Spans).
    
2. **Curation:** Seleção de prompts representativos ou mal sucedidos para compor o dataset.
    
3. **Simulation:** Re-execução do pipeline com novos hiperparâmetros ou modelos usando o dataset como _ground truth_.
    
4. **Deployment:** Implementação da melhoria com confiança estatística.
    

---

> [!IMPORTANT] **Engenharia de Confiabilidade** A capacidade de rastrear a fonte de um erro e verificar se a solução funciona (via re-teste no dataset customizado) é o que separa um chatbot instável de um produto de IA pronto para o mercado.