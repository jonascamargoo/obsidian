---
tipo: moc
area: IAs
tags:
- ia
criada: '2026-07-22'
---

# MOC — IAs

Hub da área de Inteligência Artificial. Ver também [[roadmap]].

## Fundamentos de Machine Learning

- [[KNN - Algoritmo de Classificação]] · [[Naive Bayes]] · [[Árvore de Decisão]] — classificadores clássicos
- [[Algoritmos genéticos]] (+ [[Exercicios|exercícios]]) — otimização evolutiva
- [[Lógica Fuzzy]] — raciocínio com incerteza
- [[analise de sentimentos]] e [[Pre-processamento de textos]] — NLP clássico

## Redes Neurais

- [[Fundamentos das RNAs]] → [[Perceptron]] → [[Redes Neurais Não-Lineares (função de ativação)]]
- [[Tensores]] e [[Implementação de Regressão Linear]] (PyTorch)
- [[Estrutura de Projetos em Machine Learning (Framework)]] — organização de projetos de ML

## LLMs — conceitos

- [[AI-powered applications and LLM]] — visão geral de aplicações
- [[Transformer architecture]] — a arquitetura por trás dos LLMs
- [[Context Window e lost in the middle]] · [[Controlando a Aleatoriedade da Geração em LLMs]] · [[LLM sampling strategies]]
- [[Vision Language Models (VLMs) - Arquitetura e Desafios]] — multimodalidade

## Engenharia de Prompt

- [[8 Elementos de um bom prompt]] — checklist base
- Técnicas: [[Chain-of-Thought Prompting]] · [[Prompt em dois passos]] · [[Prompts de follow-up]] · [[Verificação cognitiva]] · [[Meta-prompts]] · [[Persona do usuário]]

## RAG

- [[Retrieval-Augmented Generation (RAG)]] — ponto de partida · [[RAG vs. Fine-Tuning]]
- **Indexação**: [[Chunking]] · [[Embedding]] · [[Vector DBs]] · [[Vector Database]] · [[ANN - Escalabilidade da Busca Vetorial]]
- **Busca**: [[Semantic Search]] · [[Keyword Search]] · [[Hybrid Search]] · [[Metadata Filtering In Rag]] · [[Otimização de Consultas (Query Parsing) em RAG]]
- **Refinamento**: [[Reranking]] · [[Arquiteturas Avançadas de Busca Semântica - Cross-encoders e ColBERT]]
- **Qualidade**: [[Retrieval Quality Metrics]] · [[Avaliando a LLM no RAG]] · [[Alucinações em RAGs]] · [[Choosing model to RAG system]] · [[Engenharia de prompt em RAGs]]
- **Agentic RAG**: [[Agentic RAG]] → curso em `RAGs/Agentic RAG/` ([[Fundamentos e Arquitetura]], [[Arquitetura de Roteamento Dinâmico (Router Engine)]], [[Tool Calling e Auto-Retrieval]], [[Agent Reasoning Loop e Controle de Baixo Nível]], [[Multi-Document Agents e Arquitetura de Tool Retrieval]])
- **GraphRAG**: curso em `RAGs/Knowledge Graph/` (aulas 1–7, começar por [[1 - Deep Dive -> Knowledge Graphs para GraphRAG]])
- **Produção**: `RAGs/Rag in prod/` ([[Intro]], [[Custo vs. Performance]], [[Latência vs. Qualidade - Otimizando o Pipeline RAG]], [[Observabilidade em RAG - Métricas, Escopo e Avaliadores]], [[Quantização -  Otimizando Custo, Velocidade e Memória]], [[Security]], [[Multi Modal RAG]], [[Datasets Customizados - O Flywheel de Melhoria Contínua]], [[Hands-on - Guia de Implementação (Tracing & Telemetria)]])
- **Semantic Caching**: curso em `RAGs/Semantic Caching/` (aulas 01–06, começar por [[01 - Introducing To Semantic Caching]])

## Agentic AI

- Curso LangGraph: [[1 - Introduction to AI Agents and LangGraph]] → [[6 - Human-in-the-Loop, Controle de Estado e Time Travel]]
- [[Os-4-Tipos-de-Memoria-de-Agentes-de-IA]] — memória de agentes
- [[MCP]] — Model Context Protocol
- [[Langchain (framework)]]
