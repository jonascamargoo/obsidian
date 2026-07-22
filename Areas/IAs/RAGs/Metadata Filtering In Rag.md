---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-08-27'
---

Em sistemas de busca avançada, como o RAG (Retrieval-Augmented Generation), o "metadata filtering" (filtragem por metadados) é um mecanismo crucial de segurança, personalização e relevância.

Como o texto-base indica, a filtragem por metadados **não realiza a recuperação de dados** por si só. Em vez disso, ela **restringe os resultados** que foram obtidos por outras técnicas (como a busca vetorial semântica).

A sua principal característica é que ela opera com base em **atributos (metadados)**, e não no **conteúdo da consulta**.

### Como Funciona na Prática?

Pense no metadata filtering como os filtros de um site de e-commerce:

1. **A "Outra Técnica" (Busca Semântica):** Você digita "tênis de corrida" na barra de busca. A busca semântica entende o _significado_ e encontra 500 tênis relevantes.
    
2. **O "Metadata Filtering":** Agora, você usa os filtros na lateral: `Marca: [Nike]`, `Tamanho: [42]`, `Cor: [Preto]`.
    

O sistema não fez uma nova busca por "tênis de corrida da Nike tamanho 42". Ele simplesmente pegou os 500 resultados originais e **restringiu** a lista, mostrando apenas aqueles que tinham as "etiquetas" (metadados) correspondentes.

### Aplicado ao RAG

Em um sistema RAG, cada "chunk" (pedaço de documento) no banco vetorial possui não apenas o seu conteúdo (o vetor), mas também metadados:

- `"ano": 2023`
    
- `"departamento": "RH"`
    
- `"nivel_acesso": "Confidencial"`
    
- `"autor": "Ana Silva"`
    

Quando um usuário faz uma pergunta, o processo ocorre em duas etapas:

1. **Recuperação (Baseada no Conteúdo):** A busca vetorial encontra os 250 chunks mais relevantes para o _significado_ da pergunta (ex: "Qual o bônus de performance?").
    
2. **Filtragem (Baseada nos Atributos):** O sistema então aplica os filtros com base nos **atributos do usuário**. Se o usuário logado é do time de "Vendas", o sistema restringe os resultados, descartando todos os chunks que não sejam `nivel_acesso: "Público"` ou `departamento: "Vendas"`.
    

Em resumo, o metadata filtering não é quem _encontra_ a agulha no palheiro. Ele é o "segurança" que verifica o crachá de cada agulha que a busca vetorial encontrou, garantindo que apenas as corretas cheguem ao usuário.