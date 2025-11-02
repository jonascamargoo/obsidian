

Embora a busca vetorial (semântica) seja fundamental, sua implementação ingênua, conhecida como **k-Nearest Neighbors (k-NN)**, sofre de um grave problema de escalabilidade.

### O Problema do k-NN (Busca Exata)

O k-NN, ou "busca exata", é o algoritmo básico de recuperação vetorial.

1. **Vetorização:** O prompt e todos os documentos são vetorizados.
    
2. **Cálculo de Distância:** O vetor do prompt é comparado com **todos os outros vetores** da base de dados.
    
3. **Ordenação:** Os resultados são ordenados por distância para encontrar os `k` mais próximos.
    


![[Pasted image 20250824223907.png]]

**O Problema:** O custo computacional é $O(N)$, crescendo linearmente com o número de documentos ($N$).

- **$10^3$ documentos** = $10^3$ cálculos de distância.
    
- **$10^9$ documentos** = $10^9$ cálculos de distância (um milhão de vezes mais lento).
    

Isso torna a busca exata impraticável em _web scale_, levando a uma latência inaceitável.

Problema: é O(n), se houve 1000 documentos, a cada busca será calculado a distancia com 1000 documentos

![[Pasted image 20250824223746.png]]



## O Approximate Nearest neighbor

ANN is significantly faster than KNN; 
Rely on additional data structures; 
Not guaranteed to find the absolute closest documents


#### Navigable small world

Compute distances between all document vectores;
add one node to the graph for each documents;
connect each node to its nearest neighbors;
can traverse the graph moving along edges between neighboring documents;

Quando um prompt é recebido, ele é vetorizado para uma query vector e o objetivo é achar os documentos mais perto daquele query vector. Para isso, o algoritmo, randomicamente, escolhe um ponto de entrada chamado candidate vector para começar. É computado a distância desse vetor com os vizinhos, achando o vetor mais próximo e, em seguida, a partir da nova posição, o vetor vai atravessando para o grafo mais próximo sempre em busca do vetor mais próximo. May not find closest possible vectors, algorithm doesn't pick optmal overall path, just best part in each moment. Esse algoritmo é bem mais rapido que o KNN. Improvement: Hierarchical Navigable Samll World (HNSW) enhances Navigable Samll World by speeding up early parts of the search; Relies on hierarchical proximity graph.


How it works for 1000 docs knowledge base: 1. Layer 1 contains all 1,000 vectors with complete proximity; 2. Layer 2 randomly drop to 100 vectors and build a new proximity graph for intermediate navigation; 3. Layer 3 randomly drop to just 10 vectors and create a proximity graph for fast navigation at the highest level. Agora a segunda parte: in layer 3 choose random candidate vector and search top layer to get as close as you can in this layer; in layer 2 start at best candidate from layer 3, and complete normal search through the layer 2 proximity graph; in layer 1 start at best candidate in layer 2, and complete normal search throught the leayer 1 proximit graph

![[Pasted image 20250825083945.png]]
ANN takeaways: * ANN is significantly faster than KNN at scale; * Find close documents, but can't guarantee best matches; * Depends on proximity graph, computationally expensive to build but can pre-computed before receibing any prompts