## Definição:

Um Data Lake é um repositório de dados centralizado que armazena uma ampla variedade de dados, incluindo dados brutos (da forma que vieram), estruturados e não estruturados, em sua forma original. Diferentemente de um[ Data Warehouse](obsidian://open?vault=obsidian&file=Areas%2FBanco%20de%20dados%2FArquitetura%20de%20Dados%2FData%20Warehouse) tradicional, um Data Lake permite que organizações armazenem grandes volumes de dados sem a necessidade de uma estrutura pré-definida, o que facilita a ingestão e o processamento de dados de diversas fontes. Essa abordagem flexível possibilita análises mais abrangentes e a descoberta de insights valiosos por meio da aplicação de técnicas avançadas de processamento e análise de dados. O Data Lake é especialmente útil para lidar com dados de grande escala e para suportar aplicações que requerem uma variedade de dados, desde dados históricos até dados gerados em tempo real.

![[Pasted image 20240123091302.png]]



### Benefícios:

* Consolidação de dados em repositório central, em qualquer formato, atendendo a caso de usos de dados futuros;
* Economia de custos - são projetados para serem armazenados em hardwares comuns
* Suporte para variedade de casos de uso, podendo ser explorado por vários algoritmos para machine learning.

### Desvantagens:

- Desempenho insatisfatório para casos de uso de BI, com um tempo de consulta maior
- A falta de consistência pode causar problemas de seguranças, já que o controle é menor







![[Pasted image 20240123092008.png]]