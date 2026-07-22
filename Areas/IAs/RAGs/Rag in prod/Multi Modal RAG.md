---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/llmops
criada: '2026-02-24'
---

**Data:** 24/02/2026 **Tópico:** #Multimodal #ComputerVision #RAG #VectorDatabase #LLMOps

---

## 🧩 1. Arquitetura do RAG Multimodal

O RAG não precisa mais se limitar a dados em formato de texto puro. Um sistema RAG multimodal típico é projetado para aceitar tanto textos quanto imagens como prompts.

- Ele armazena arquivos de texto e imagem diretamente na base de conhecimento.
    
- O sistema processa essas múltiplas modalidades e, ao final, gera respostas em texto.
    
- Para que essa arquitetura funcione, tanto o modelo de _embedding_ quanto o LLM precisam ser atualizados para possuir capacidades multimodais.
    

---

## 🌌 2. Modelos de Embedding Multimodal

A principal inovação na etapa de recuperação é o modelo de _embedding_ multimodal.
![[Pasted image 20260224003629.png]]
- Esses modelos conseguem embutir múltiplos formatos de dados dentro do mesmo espaço vetorial.
    
- Se você fornecer a palavra "cachorro" e a imagem de um cachorro, o modelo colocará ambos os vetores muito próximos no espaço vetorial.
    
- Se você fornecer a imagem de uma árvore e a palavra "árvore", eles também ficarão próximos entre si, mas em uma região diferente dos vetores relacionados a cachorros.
    
- A busca vetorial opera da mesma maneira que no RAG de texto, retornando as imagens ou documentos cujos vetores possuam a menor distância matemática em relação ao vetor do prompt.
    

---

## 👁️‍🗨️ 3. Language Vision Models (LLMs Visuais)

Para o processo de síntese e geração, utiliza-se um _Language Vision Model_.
![[Pasted image 20260224003904.png]]
- Esse tipo de modelo funciona de maneira muito semelhante a um LLM focado apenas em texto, mas possui a capacidade adicional de processar imagens tokenizadas.
    
- Para tokenizar uma imagem, o processo típico envolve dividi-la em "patches" (quadros menores), onde cada quadro é representado como um token individual.
    
- Dependendo da resolução da imagem, ela pode ser representada por cerca de 100 tokens até quase 1.000 tokens.
    
- O _transformer_ do modelo recebe essa sequência multimodal de tokens, desenvolve um entendimento sobre as relações entre os textos e as imagens do prompt, e gera a resposta final em texto.
    

---

## 📄 4. O Desafio da Densidade (PDFs e Slides)

A vantagem de habilitar o sistema para imagens é a facilidade de ingestão de formatos comuns, já que PDFs e slides podem ser facilmente tratados como arquivos de imagem.

- O grande desafio de engenharia nesses formatos é a extrema densidade de informações.
    
- Uma única página pode conter simultaneamente textos, gráficos, imagens e legendas.
    
- Um único vetor teria grande dificuldade em capturar todas as nuances e detalhes presentes em uma página inteira de PDF.
    
- Inicialmente, tentou-se usar algoritmos complexos de detecção para separar os gráficos dos textos, mas essas técnicas provaram ser muito propensas a falhas na prática.
    

---

## 🔲 5. A Solução: Grid Chunking e ColBERT

Para contornar o problema de detecção falha, surgiu uma abordagem chamada _PDF RAG_.

- Em vez de tentar entender o layout da página, o sistema simplesmente divide cada página em um "grid" de quadrados.
    
- O sistema não se importa se os limites dos quadrados cortam elementos em locais inapropriados.
    
- Cada quadrado é então embutido em um vetor denso utilizando o modelo de _embedding_ multimodal.
    
- Consequentemente, uma única página de PDF passa a ser representada por milhares de vetores.
    
- A busca vetorial funciona de forma semelhante à arquitetura ColBERT: cada palavra no prompt busca o quadrado que melhor corresponde a ela na página.
    
- Essas pontuações individuais são somadas para fornecer a pontuação de relevância global da página do documento.
    

> [!WARNING] **Trade-off de Infraestrutura** Embora a abordagem de divisão em _grid_ seja muito flexível e apresente ótimo desempenho em recuperação, sua principal desvantagem é exigir que o banco de dados vetorial armazene uma quantidade massiva de vetores.