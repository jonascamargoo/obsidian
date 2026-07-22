---
tipo: projeto
area: TCC
tags:
- tcc
criada: '2026-04-20'
---

## 1. Definição do Problema

O armazenamento de modelos biométricos (_embeddings_) originais representa um risco crítico de segurança, pois a biometria é um identificador imutável. No contexto de regulamentações como o **ECA Digital**, existe a necessidade de verificar atributos (ex: idade > 18) sem expor ou armazenar a identidade real do utilizador. A **Biometria Cancelável** surge como uma solução para gerar templates que podem ser revogados e que não permitem a reconstrução da imagem original.

### Pergunta de Pesquisa:

> _"Qual é o impacto da aplicação de Projeções Aleatórias na acurácia de um sistema de reconhecimento facial comparado ao uso de embeddings biométricos originais?"_

---

## 2. Objetivos do Projeto

### Objetivo Geral

Realizar um estudo comparativo entre um sistema de reconhecimento facial convencional e um sistema protegido por técnicas de biometria cancelável, avaliando o compromisso técnico entre **privacidade** e **precisão**.

### Objetivos Específicos

1. **Extração de Características:** Utilizar modelos pré-treinados para converter imagens de faces em vetores numéricos (_embeddings_).
    
2. **Implementação da Proteção:** Aplicar o algoritmo de **Projeções Aleatórias** (Random Projections) para transformar os vetores originais em templates protegidos e não-inversíveis.
    
3. **Avaliação de Acurácia:** Comparar as taxas de erro (FAR e FRR) entre o sistema original e o sistema com biometria cancelável.
    
4. **Análise de Segurança:** Demonstrar teoricamente por que a transformação aplicada impede a recuperação do dado biométrico original em caso de vazamento da base de dados.

---

## 3. Metodologia Simplificada (O "Caminho Feliz")

O trabalho será conduzido como um experimento controlado em ambiente Python:

1. **Dataset:** Utilização de uma base de dados pública e consolidada (ex: _Labeled Faces in the Wild - LFW_).
    
2. **Extração:** Uso da biblioteca `DeepFace` para gerar os vetores de características de forma automatizada.
    
3. **Transformação:** Implementação de uma matriz de projeção aleatória estável (usando `scikit-learn` ou `NumPy`) para gerar os templates canceláveis.
    
4. **Comparação:** Execução de testes de correspondência (_matching_) para verificar se o sistema ainda reconhece a mesma pessoa após a "distorção" matemática do vetor.
---

## 4. Métricas de Avaliação

Os resultados serão apresentados através de métricas clássicas de sistemas biométricos e segurança:

- **Curva ROC (Receiver Operating Characteristic):** Para visualizar o desempenho global dos dois modelos.
    
- **EER (Equal Error Rate):** O ponto onde os erros de falsa aceitação e falsa rejeição se equilibram.
    
- **Análise de Irreversibilidade:** Justificativa matemática da dificuldade computacional de inverter a matriz de projeção sem a chave original.