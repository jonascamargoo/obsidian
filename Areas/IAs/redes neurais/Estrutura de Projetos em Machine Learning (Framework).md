
Este material resume o fluxo de trabalho sistemático (pipeline) utilizado para criar modelos de Inteligência Artificial, ilustrado através do problema de **previsão de tempo de entrega**.

### Conceito Chave: Inferência

Antes de iniciar o pipeline, é importante definir o objetivo final. Após o modelo encontrar padrões nos dados históricos, usamos esse modelo treinado para fazer previsões em **novos dados** (locais de clientes que o modelo nunca viu antes).

> **Definição:** O processo de usar um modelo treinado para fazer previsões em dados não vistos é chamado de **Inferência**.

---

## 🛠️ As 6 Etapas do Framework de Machine Learning

Independentemente de você estar prevendo tempos de entrega, classificando imagens ou analisando textos, a estrutura subjacente do projeto segue estas seis etapas fundamentais:
![[Pasted image 20251216170819.png]]

### Estágio 1: Ingestão de Dados (Data Ingestion)

Tudo começa com os dados. Antes do treinamento, é necessário reunir a informação bruta.

- **Fonte:** Para o nosso exemplo, os dados vêm dos registros de entrega da empresa.
    
- **Desafio:** Dados do mundo real são "sujos" e desorganizados.
    
    - _Exemplos de problemas:_ Entradas de texto livre (ex: "22 minutos") misturadas com números (ex: "22.0"), valores ausentes, ou dados impossíveis (ex: entregas feitas a 300 km/h).
        
- **Nota:** Neste curso, começaremos com dados limpos para facilitar, mas no mundo real, lidar com dados bagunçados é a norma, não a exceção.
    ![[Pasted image 20251216171247.png]]

### Estágio 2: Preparação dos Dados (Data Preparation)

Obter os dados é apenas o início. Agora é preciso limpar, transformar e organizar para que o PyTorch possa processá-los.

- **Limpeza:** Remover erros, como tempos de entrega impossíveis ou entradas duplicadas.
    
- **Tratamento:** Lidar com valores ausentes (ex: carimbos de data/hora não registrados).
    
- **Engenharia de Features (Feature Engineering):** Converter dados brutos em formatos úteis.
    
    - _Exemplo:_ Converter um endereço de texto ("Rua das Flores, 123") em uma distância numérica ("8.2 milhas").
        

> **Importante:** Esta etapa geralmente consome a maior parte do tempo e código em um projeto real. Modelos falham mais frequentemente devido a dados ruins do que devido a matemática errada.
> ![[Pasted image 20251216171349.png]]

### Estágio 3: Construção do Modelo (Model Building)

Com os dados prontos, projetamos a arquitetura que aprenderá com eles.

- **Arquitetura:** Refere-se à estrutura do modelo. Quantos neurônios? Como eles se conectam? Quais tipos de camadas?
    
- **No nosso exemplo:** A arquitetura é simples — um único neurônio que aprende a relação linear entre _distância_ e _tempo_.
    
- **PyTorch:** Definir essa arquitetura pode levar apenas uma única linha de código, mas segue os mesmos princípios de modelos complexos.
    ![[Pasted image 20251216171637.png]]

### Estágio 4: Treinamento (Training)

É aqui que o modelo realmente aprende. O modelo recebe exemplos (ex: "8.2 milhas demorou 22 minutos") e ajusta seus parâmetros gradualmente para entender o padrão.

- **Componentes Chave:**
    
    1. Medir o erro da previsão.
        
    2. Guiar o modelo para melhorar.
        
    3. Controlar a velocidade de aprendizado.
        
- O PyTorch executa o "loop de treinamento" (training loop) para realizar o trabalho pesado de cálculo.
    ![[Pasted image 20251216171552.png]]

### Estágio 5: Avaliação e Depuração (Evaluation and Debugging)

O sucesso no treinamento não garante sucesso no mundo real. Precisamos testar se o modelo **generaliza** bem.

- **Conjunto de Teste (Test Set):** Uma porção dos dados que foi separada e **não** foi usada durante o treinamento.
    
- **O Teste:** O modelo faz previsões nesses dados "invisíveis" e comparamos com a realidade.
    
    - _Exemplo:_ O modelo previu 28 minutos, mas a realidade foi 32 minutos. Quão próximo ele chegou?
        
- **Objetivo:** Determinar se o modelo é confiável o suficiente para ser usado.
    

### Estágio 6: Implantação (Deployment)

A etapa final é colocar o modelo no mundo real para as pessoas usarem.

- _Nota:_ Por enquanto, deixaremos esta etapa de fora para focar na construção e validação do modelo nas etapas anteriores.
    

---
