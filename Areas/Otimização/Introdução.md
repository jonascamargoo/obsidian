---
tipo: conceito
area: Otimização
tags:
- matematica/otimizacao
criada: '2025-04-07'
---

## 🎯 O que é Otimização?

A otimização é um ramo da matemática aplicada e da ciência da computação que estuda métodos para encontrar a **melhor solução possível** para um problema, dentro de um conjunto de alternativas viáveis.

- **Objetivo principal**: Maximizar ou minimizar uma função (chamada de função objetivo), respeitando determinadas **restrições**.
    
- **Exemplos práticos**:
    - Maximizar o lucro de uma empresa
    - Minimizar o custo de produção
    - Minimizar o tempo de resposta de um algoritmo
        

> 💡 **Insight**: Muitos problemas do mundo real envolvem otimização — da logística à engenharia, da economia à inteligência artificial.


## 📌 Componentes de um Problema de Otimização

1. **Variáveis de decisão**
    - São as incógnitas do problema, ou seja, o que você quer descobrir.
    - Exemplo: quantidade de produto a ser fabricado.
        
2. **Função objetivo**
    - Expressa o que se quer **maximizar** ou **minimizar**.
    - Exemplo: lucro, tempo, distância, custo.
        
3. **Restrições**
    - Regras que limitam as possíveis soluções.
    - Exemplo: capacidade de produção, orçamento, tempo disponível.
        

> ⚠️ Correção comum: Algumas fontes confundem função objetivo com equação de restrição. A função objetivo é **única** e expressa o **desejo do problema**. As restrições são condições que a solução precisa respeitar.

## 📈 Classificações de Problemas de Otimização

- **Linear vs. Não Linear**
    - Linear: todas as equações (objetivo e restrições) são lineares.
    - Não linear: pelo menos uma equação tem termos quadráticos, exponenciais, logarítmicos etc.
        
- **Contínuo vs. Discreto**
    - Contínuo: variáveis podem assumir qualquer valor real dentro de um intervalo.
    - Discreto (ou inteiro): variáveis assumem valores inteiros (frequente em alocação e logística).
        
- **Determinístico vs. Estocástico**
    - Determinístico: todos os parâmetros são conhecidos com certeza.
    - Estocástico: existe incerteza (ex: demanda futura, tempo de entrega).


📌 Insight: Muitos problemas industriais são **lineares inteiros mistos**, onde parte das variáveis é contínua e parte é inteira.

## 📐 Exemplo Clássico: Problema da Dieta

> Qual é a combinação mais barata de alimentos que atende às necessidades nutricionais de uma pessoa?

- **Variáveis**: quantidade de cada alimento
- **Objetivo**: minimizar o custo
- **Restrições**: garantir ingestão mínima de proteínas, calorias, vitaminas etc.
    

> 💬 Insight: Esse problema originou o desenvolvimento da programação linear por George Dantzig!


## ⚙️ Métodos de Resolução

### 🔹 Métodos Exatos

- Garante a solução ótima
- Exemplo: Simplex, Branch and Bound
- Usado quando a dimensão do problema permite
    

### 🔹 Métodos Heurísticos

- Encontra **boas soluções**, mas não necessariamente as melhores
- Exemplo: Algoritmos Genéticos, Simulated Annealing
    

### 🔹 Métodos Metaheurísticos

- Generalizações de heurísticas, aplicáveis a múltiplos problemas
- Exemplo: Particle Swarm Optimization, GRASP
    

> 💡 Insight: Heurísticas são muito utilizadas quando o problema é grande ou mal definido — por exemplo, em IA e análise de dados.


## 💭 Aplicações Práticas

- **Transporte e Logística**: Roteirização, escalonamento
- **Engenharia**: Projeto de estruturas, processos químicos
- **Economia e Finanças**: Carteiras de investimento, precificação
- **IA e Machine Learning**: Ajuste de hiperparâmetros, redes neurais

A modelagem matemática de problemas de otimização envolve **abstrair o mundo real** para o papel. Isso exige:

- Clareza dos objetivos
- Conhecimento das restrições
- Interpretação correta da solução
    

> 📢 **Dica**: Sempre comece com um diagrama, esboço ou descrição clara do problema. Isso evita modelagens mal formuladas!