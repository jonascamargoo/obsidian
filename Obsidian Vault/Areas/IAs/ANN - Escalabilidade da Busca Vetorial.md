

> [!info] Veja também
> Este arquivo trata da **escalabilidade** do KNN em produção (busca vetorial / RAG / embeddings). Para o KNN como **algoritmo de classificação supervisionada** (com K vizinhos, distâncias Minkowski, padronização, escolha de K, etc.), veja [[KNN - Algoritmo de Classificação]].

Embora a busca vetorial (semântica) seja fundamental, sua implementação ingênua, conhecida como **k-Nearest Neighbors (k-NN)**, sofre de um grave problema de escalabilidade.

### O Problema do k-NN (Busca Exata)

O k-NN, ou "busca exata", é o algoritmo básico de recuperação vetorial.

1. **Vetorização:** O prompt e todos os documentos são vetorizados.
    
2. **Cálculo de Distância:** O vetor do prompt é comparado com **todos os outros vetores** da base de dados.
    
3. **Ordenação:** Os resultados são ordenados por distância para encontrar os `k` mais próximos.
    


![[Pasted image 20250824223907.png]]

OBS: os dados precisam estar normalizados

**O Problema:** O custo computacional é $O(N)$, crescendo linearmente com o número de documentos ($N$).

- **$10^3$ documentos** = $10^3$ cálculos de distância.
    
- **$10^9$ documentos** = $10^9$ cálculos de distância (um milhão de vezes mais lento).
    

Isso torna a busca exata impraticável em _web scale_, levando a uma latência inaceitável.

Problema: é O(n), se houve 1000 documentos, a cada busca será calculado a distancia com 1000 documentos

![[Pasted image 20250824223746.png]]

### A Solução: Approximate Nearest Neighbors (ANN)

Para resolver isso, usamos algoritmos de **Approximate Nearest Neighbors (ANN)**.

- **O Conceito:** ANN troca uma pequena quantidade de **precisão** (a garantia de encontrar o vizinho _exato_) por uma enorme melhoria em **velocidade**.
    
- **O Objetivo:** Não encontrar o vizinho _exato_, mas sim um vizinho "muito próximo", de forma muito mais rápida.
    
- **Como:** ANN usa estruturas de dados inteligentes, pré-computadas, para evitar a busca exaustiva.


### Um Algoritmo ANN: Navigable Small World (NSW)

Uma família popular de algoritmos ANN é baseada em **grafos de proximidade**. O **Navigable Small World (NSW)** é um exemplo fundamental.

#### 1. Pré-computação: Construção do Grafo

O passo mais caro é feito offline (antes de qualquer busca):

1. **Cálculo de Distância:** A distância entre cada vetor  e seu vizinho é calculada (sei o valor das arestas).
    
2. **Criação dos Nós:** Cada documento (vetor) se torna um nó no grafo.
    
3. **Criação das Arestas:** Cada nó é conectado (por uma aresta) aos seus vizinhos mais próximos.
    

O resultado é uma estrutura de grafo semelhante a uma teia, onde "saltar" por uma aresta leva a um documento semanticamente similar.

![[Pasted image 20251102113009.png]]
#### 2. Busca no Grafo (Navegação)

Quando um prompt é recebido:

1. **Vetorização:** O prompt é vetorizado (o "vetor de consulta").
    
2. **Ponto de Entrada:** Um nó de entrada aleatório é escolhido no grafo (o "candidato" inicial).
	![[Pasted image 20251102114647.png]]
    
3. Navegação Gulosa (Greedy):
    
    a. O algoritmo compara o vetor de consulta com todos os vizinhos do nó candidato atual (um número pequeno de cálculos).
    
    b. O vizinho que estiver mais próximo do vetor de consulta torna-se o novo candidato.
	![[Pasted image 20251102114739.png]]    
1. **Repetição:** O passo 3 é repetido. A busca "salta" de nó em nó, sempre se movendo para o vizinho mais próximo da consulta.
	![[Pasted image 20251102114756.png]]
    
2. **Convergência:** O processo para quando o algoritmo atinge um candidato onde _nenhum_ de seus vizinhos está mais perto da consulta do que ele mesmo. Esse candidato é o resultado retornado.
	![[Pasted image 20251102114846.png]]    

A busca é rápida porque, a cada passo, ela só calcula a distância para um pequeno número de vizinhos, em vez de para todos os $N$ documentos. A desvantagem é que ela pode cair em um "mínimo local" (não encontrando o melhor resultado global), mas na prática, os resultados são quase sempre bons o suficiente.

Pode não encontrar os vetores mais próximos possíveis; o algoritmo não escolhe o caminho ótimo em geral, apenas a melhor parte em cada momento.

### A Otimização: Hierarchical Navigable Small World (HNSW)

O **HNSW** é uma otimização do NSW que acelera drasticamente a fase inicial da busca, permitindo "saltos" maiores pelo grafo.

#### 1. Pré-computação: O Grafo Hierárquico

O HNSW constrói múltiplos grafos de proximidade em camadas, como uma pirâmide:

- **Camada 1 (Base):** Contém **todos os 1.000** vetores e seu grafo de proximidade completo.
    
- **Camada 2:** Contém um subconjunto aleatório (ex: **100** vetores) e um grafo de proximidade _apenas_ para eles.
    
- **Camada 3 (Topo):** Contém um subconjunto ainda menor (ex: **10** vetores) e seu próprio grafo.
	![[Pasted image 20251102120441.png]]

#### 2. Busca na Hierarquia

A busca agora acontece de cima para baixo:

1. **Entrada no Topo:** A busca começa em um ponto aleatório na **Camada 3** (a menor). O algoritmo navega por esta camada até encontrar o candidato mais próximo da consulta _dentro da Camada 3_.
    
2. **Descida para Camada 2:** O melhor candidato da Camada 3 é usado como _ponto de entrada_ para a busca na **Camada 2**. A busca continua na Camada 2 até encontrar o melhor candidato _nela_.
    
3. **Descida para Camada 1:** O melhor candidato da Camada 2 é usado como _ponto de entrada_ para a busca na **Camada 1** (a base completa).
    
4. **Resultado Final:** A busca navega pela Camada 1 até convergir, e o candidato final desta camada é o resultado retornado.
    ![[Pasted image 20251102120709.png]]

Esta abordagem é extremamente eficiente porque os "saltos" nas camadas superiores permitem que a busca chegue rapidamente à "vizinhança" correta. Quando ela finalmente chega à Camada 1 (onde estão todos os dados), ela já está muito próxima do vetor de destino.

### Implicações

- **Velocidade:** O HNSW transforma a complexidade de tempo de $O(N)$ (linear) do k-NN para aproximadamente **$O(\log N)$** (logarítmica). Isso permite que bancos de dados com bilhões de vetores respondam em milissegundos.
    
- **Trade-off:** É uma busca **aproximada**, sem garantia matemática de encontrar o melhor resultado absoluto.
    
- **Custo de Indexação:** A construção do grafo HNSW (indexação) é um processo computacionalmente intensivo que deve ser pré-computado.

![[Pasted image 20250825083945.png]]


Uma dúvida que pode surger é: se eu preciso buscar na camada inferior, por que não começar direto dela?  Um nó (vetor) pode **participar de múltiplas camadas**. As camadas são, na verdade, _diferentes conjuntos de conexões (arestas)_ sobre o _mesmo_ conjunto de nós.

O fluxo da **Camada 3 (Topo)** para a **Camada 2 (Meio)** acontece em três fases:

1. A Busca _na_ Camada 3.
    
2. A Transição (o "Drop Down").
    
3. A Busca _na_ Camada 2.
    

#### 1. Fase 1: Busca na Camada 3 

- **Objetivo:** Encontrar o nó _participante da Camada 3_ que esteja mais próximo do Vetor de Consulta.
    
- **Estado Inicial:** O algoritmo começa em um **ponto de entrada** pré-definido (o "entry point" da Camada 3). Vamos chamá-lo de `Node_Start`.
    
- **Processo (Loop de Busca Gulosa):**
    
    1. O algoritmo mantém uma "lista de candidatos" (uma priority queue), ordenada pela distância até o Vetor de Consulta. Inicialmente, ela contém apenas o `Node_Start`.
        
    2. O algoritmo "visita" o melhor item da lista (o nó mais próximo do vetor de consulta encontrado até agora). Vamos chamá-lo de `Current_Best`.
        
    3. **Ponto Crítico:** O algoritmo acessa a **lista de vizinhos da Camada 3** do nó `Current_Best`. (Lembre-se: este nó também tem listas para as camadas 2 e 1, mas elas são **ignoradas** nesta fase).
        
    4. Para cada `Neighbor_L3` nessa lista, o algoritmo calcula sua distância até o Vetor de Consulta.
        
    5. Se um `Neighbor_L3` for mais próximo do que o pior item na lista de candidatos (e ainda não tiver sido visitado), ele é adicionado à lista.
        
    6. O algoritmo repete os passos 2-5, sempre "pulando" para o vizinho (usando _apenas_ as conexões da Camada 3) que o aproxima mais do Vetor de Consulta.
        
- **Resultado da Fase 1:** O loop termina quando o algoritmo não consegue encontrar nenhum vizinho (nas conexões da Camada 3) que seja mais próximo do Vetor de Consulta do que o melhor candidato que ele já tem. Esse nó final é o **ótimo local** da Camada 3.
    
    - **`BestNode_L3`** = O nó na Camada 3 mais próximo do Vetor de Consulta que a busca gulosa conseguiu encontrar.
        

---

### 2. Fase 2: A Transição ("Drop Down")

- **Objetivo:** Passar o controle para a próxima camada de forma inteligente.
    
- **Processo:** Este é o passo mais simples:
    
    1. O nó `BestNode_L3` (que é o resultado da Fase 1) é selecionado.
        
    2. Como este nó (por definição de construção) também **participa** da Camada 2, ele serve como o **ponto de entrada ideal** para a busca na Camada 2.
        
    3. Ele é o "aeroporto" que a via expressa (Camada 3) nos deixou, e agora vamos começar a procurar pelas "avenidas regionais" (Camada 2) _a partir desse ponto_.
        

---

### 3. Fase 3: Busca na Camada 2 (As "Avenidas Regionais")

- **Objetivo:** Encontrar o nó _participante da Camada 2_ que esteja mais próximo do Vetor de Consulta, **começando de onde a Camada 3 parou**.
    
- **Estado Inicial:** O algoritmo cria uma **nova lista de candidatos**. O único item nessa lista é o `BestNode_L3` (o resultado da Fase 2).
    
- **Processo (O _Mesmo_ Loop, _Outras_ Conexões):**
    
    1. O algoritmo "visita" o melhor item da lista (inicialmente, o `BestNode_L3`). Vamos chamá-lo de `Current_Best_L2`.
        
    2. **Ponto Crítico:** O algoritmo acessa a **lista de vizinhos da Camada 2** do nó `Current_Best_L2`. (Esta lista é _diferente_ e mais densa que a lista da Camada 3 do mesmo nó).
        
    3. Para cada `Neighbor_L2` nessa lista, o algoritmo calcula sua distância até o Vetor de Consulta.
        
    4. (O mesmo processo de antes...) Se um `Neighbor_L2` for melhor, ele é adicionado à lista de candidatos.
        
    5. O algoritmo repete os passos, navegando pela Camada 2.
        
- **Resultado da Fase 3:** O loop termina quando o algoritmo não consegue encontrar nenhum vizinho (usando _apenas_ as conexões da Camada 2) que o aproxime mais do Vetor de Consulta.
    
    - **`BestNode_L2`** = O nó na Camada 2 mais próximo do Vetor de Consulta.
        

Este `BestNode_L2` será, então, usado como o ponto de entrada para a busca final na Camada 1 (a base completa).