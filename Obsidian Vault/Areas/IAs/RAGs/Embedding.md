O trabalho de um modelo de embedding parece simples: transformar textos similares em vetores (pontos) que fiquem próximos, e transformar textos diferentes em vetores que fiquem distantes.

Mas como um computador aprende a fazer isso? O processo é sofisticado e se baseia em uma técnica chamada **Treinamento Contrastivo** (Contrastive Training).

### O Conceito: Pares Positivos e Negativos

O treinamento funciona dando ao modelo exemplos do que "acertar" e do que "errar".

- **Par Positivo:** Dois pedaços de texto similares que devem ficar _próximos_.
    
    - Ex: `"bom dia"` e `"olá"`
        
- **Par Negativo:** Dois pedaços de texto diferentes que devem ficar _distantes_.
    
    - Ex: `"bom dia"` e `"isso é um trombone barulhento"`
        

O objetivo do treinamento é "puxar" os pares positivos para perto e "empurrar" os pares negativos para longe.

![[Pasted image 20251031123512.png]]

---

### A Implementação Prática: Sentence Transformers

Essa teoria do treinamento contrastivo tem uma implementação prática muito famosa: os **Sentence Transformers** (também conhecidos como SBERT).

Esses modelos usam uma arquitetura específica, muitas vezes chamada de **Rede Triplet (Triplet Network)**, para executar esse treinamento de forma eficiente. Em vez de apenas pares, o modelo processa três frases de uma vez:

1. **Âncora:** "ele podia sentir o cheiro das rosas"
    
2. **Positiva:** "um campo de flores perfumadas"
    
3. **Negativa:** "um leão rugiu majestosamente"
    

O modelo gera vetores para os três. Seu objetivo matemático é **minimizar** a distância entre a Âncora e a Positiva, enquanto **maximiza** a distância entre a Âncora e a Negativa. É exatamente assim que o "puxa-empurra" é implementado no código.

---

### O Processo de Treinamento

O treinamento é um processo iterativo que ajusta o modelo lentamente:

1. **Compilação da Base de Treino:** O primeiro passo é reunir uma coleção massiva de dados. Esta é a **"base de treino"** (training set) — o conjunto de dados que o modelo tem permissão para "ver" e usar para aprender. Ela é composta por milhões de "triplets" (âncora, positivo, negativo).
    
2. **Início Aleatório:** No começo, o modelo é "burro". Ele atribui a cada pedaço de texto um **vetor aleatório**. Esses vetores não significam nada e, se usados para busca, retornariam resultados sem sentido.
    
3. **Avaliação:** O modelo então olha para os triplets na sua **base de treino** e pergunta: "O quão bem eu posicionei os pares positivos juntos e os pares negativos separados?"
    
4. **Ajuste:** Com base em seu desempenho, o modelo atualiza seus parâmetros internos para tentar atingir seu objetivo (minimizar distância positiva, maximizar negativa).
    
5. **Repetição:** O processo é repetido milhões de vezes (usando apenas a base de treino), atualizando os vetores, reavaliando o desempenho e ajustando os parâmetros novamente.

	![[Pasted image 20251031124203.png]]
	![[Pasted image 20251031124520.png]]

	OBS: a âncora nesse caso é o item vermelho, positivo é o verde e negativo o roxo
### Validando o Aprendizado: A Base de Teste

Mas como sabemos que o modelo realmente _aprendeu_ o conceito de "significado" e não apenas _decorou_ os exemplos da base de treino? (Um problema chamado _overfitting_).

É aqui que entra a **"base de teste"** (test set). Este é um conjunto de dados completamente separado (também com triplets) que o modelo **nunca viu** durante o treinamento.

Após o término do treinamento, os engenheiros usam essa base como uma "prova final". Se o modelo conseguir agrupar corretamente os pares positivos e afastar os negativos da base de teste, ele provou que pode **generalizar** seu conhecimento para textos novos.

---

### A "Bagunça" Organizada e as Várias Dimensões

Na prática, esse processo é caótico. Cada vetor no espaço é simultaneamente um "ponto âncora", um "exemplo positivo" para alguns vetores e um "exemplo negativo" para milhões de outros.

Cada ponto está sendo **puxado e empurrado em milhares de direções ao mesmo tempo**.

É por isso que os modelos usam vetores com centenas ou milhares de dimensões (ex: 768, 1536). Um espaço de alta dimensão dá ao algoritmo muito "espaço de manobra" para organizar esses pontos de forma que todas essas relações complexas de significado sejam respeitadas.

---

### O Que Você Realmente Precisa Saber

Você não precisa treinar um modelo do zero, mas entender como ele funciona nos ensina duas lições cruciais:

1. **O Significado é um "Cluster" (Aglomerado)** O significado não está em um local específico do espaço. Em vez disso, o treinamento forma **"aglomerados"** de conceitos. Haverá um "bairro" no espaço vetorial para conceitos sobre "leões" e outro bairro para conceitos sobre "trombones".
    
2. **A Regra de Ouro: Nunca Compare Vetores de Modelos Diferentes** Esta é a lição mais importante. Você **só pode comparar vetores gerados pelo mesmo modelo de embedding**.
    
    - Cada modelo (seja `OpenAIEmbeddings` ou um `SentenceTransformer`) foi treinado com dados diferentes, dimensões diferentes e, o mais importante, com **valores aleatórios iniciais diferentes**.
        
    - Tentar encontrar a distância entre um vetor do Modelo A e um vetor do Modelo B é como comparar coordenadas de GPS de dois planetas diferentes. O resultado é um completo absurdo.