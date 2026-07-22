---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-03-18'
---

## O que é RAG?

Retrieval-Augmented Generation (RAG) é um processo que melhora a saída de um grande modelo de linguagem (LLM), permitindo que ele acesse bases de conhecimento externas antes de gerar uma resposta. Os LLMs são treinados em grandes volumes de dados e utilizam bilhões de parâmetros para realizar tarefas como responder perguntas, traduzir idiomas e gerar textos.

A abordagem RAG estende as capacidades dos LLMs, tornando-os mais precisos e relevantes para domínios específicos ou bases de conhecimento internas, sem a necessidade de re-treinamento. Dessa forma, é possível otimizar o desempenho do modelo de maneira econômica e eficiente.

## Importância da RAG

Os LLMs enfrentam desafios como:

- **Fornecimento de informações falsas** quando não possuem uma resposta adequada.
    
- **Uso de dados desatualizados** ou genéricos para responder perguntas específicas.
    
- **Dependência de fontes não confiáveis**.
    
- **Confusão terminológica**, quando diferentes fontes utilizam a mesma terminologia para conceitos distintos.
    

A RAG soluciona esses problemas ao recuperar dados relevantes de fontes confiáveis antes de gerar respostas, aumentando o controle e a confiabilidade das respostas geradas.

## Benefícios da RAG

### Implementação econômica

A criação de chatbots e sistemas de IA generativa normalmente utiliza modelos de base (FMs), treinados com grandes volumes de dados generalizados. Atualizar esses modelos para incluir informações específicas pode ser muito caro. A RAG permite integrar novos dados ao LLM de forma mais acessível, tornando a tecnologia mais viável economicamente.

### Informações atualizadas

Os dados de treinamento dos LLMs podem se tornar obsoletos. Com a RAG, é possível conectar o modelo a fontes de informação atualizadas, como sites de notícias, bases de dados corporativas e APIs.

### Maior confiança dos usuários

A RAG permite que os LLMs apresentem respostas mais confiáveis, citando as fontes utilizadas. Isso aumenta a transparência e credibilidade da IA, permitindo que os usuários consultem as referências das respostas fornecidas.

### Maior controle no desenvolvimento

Com a RAG, as equipes de desenvolvimento podem:

- Modificar e gerenciar fontes de informação conforme necessário.
    
- Restringir acesso a dados sensíveis com base em permissões.
    
- Corrigir informações incorretas ou atualizar fontes rapidamente.
    

![[Pasted image 20250318140907.png]]

## Como funciona a RAG?

### 1. Criação de dados externos

Os dados externos são informações que não fazem parte do treinamento original do LLM. Podem ser obtidos de fontes como APIs, bancos de dados ou repositórios de documentos. Esses dados são transformados em representações numéricas e armazenados em um banco de dados vetorial, tornando-se acessíveis ao modelo de IA.

### 2. Recuperação de informações relevantes

Quando um usuário faz uma consulta, o sistema converte a pergunta em uma representação vetorial e a compara com os dados armazenados no banco de vetores. Assim, ele recupera os documentos mais relevantes para a questão. É importante notar que o prompt também passa pelo modelo de embedding em questão.

![[Pasted image 20251031114648.png]]

### 3. Enriquecimento do prompt

Os dados recuperados são adicionados ao prompt enviado ao LLM, garantindo que ele tenha um contexto mais preciso para gerar a resposta. Essa técnica melhora a qualidade e precisão das respostas geradas.

### 4. Atualização dos dados externos

Para manter a relevância das informações, os documentos e suas representações vetoriais podem ser atualizados regularmente. Isso pode ser feito em tempo real ou em lotes periódicos, garantindo que as respostas geradas estejam sempre baseadas nos dados mais recentes.


## Exemplo real de fluxo RAG

Vamos considerar um chatbot de suporte ao cliente de um banco que utiliza RAG para responder perguntas sobre políticas de cartões de crédito.

1. **Usuário faz uma pergunta**: "Qual a taxa de anuidade do cartão Gold?"
    
2. **Recuperação de dados**: O sistema busca documentos recentes no banco de dados interno contendo informações sobre taxas de anuidade de diferentes cartões.
    
3. **Enriquecimento do prompt**: O modelo recebe a pergunta do usuário junto com as informações recuperadas, como: "O cartão Gold tem uma anuidade de R$ 300,00, podendo ser parcelada em 12x de R$ 25,00."
    
4. **Geração da resposta**: O LLM processa a pergunta com o contexto recuperado e responde: "A taxa de anuidade do cartão Gold é de R$ 300,00, podendo ser parcelada em 12x de R$ 25,00. Essa informação está disponível na página oficial de tarifas do banco."
    
5. **Atualização contínua**: Sempre que houver mudanças nas taxas, o banco de dados é atualizado e as representações vetoriais são refeitas para refletir as novas informações.


## Conclusão

A Retrieval-Augmented Generation (RAG) é uma abordagem poderosa para melhorar a precisão, confiabilidade e atualização dos LLMs sem a necessidade de re-treinamento extensivo. Ao permitir que os modelos acessem fontes de conhecimento externas, a RAG se torna uma solução eficaz para aprimorar aplicações de IA generativa em diversos contextos.