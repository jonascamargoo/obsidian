
![[Pasted image 20230706220716.png]]

#### Análise com exemplo
Suponha que queiramos armazenar os dados referentes aos alunos
de uma determinada turma que ingressaram em um curso específico.
Cada aluno é identificado unicamente pela sua matrícula. O número de matrícula dos alunos é dado por uma seqüência de 8 dígitos:

```
struct aluno {
    int mat;             // 4 bytes
    char nome[81];       // 1 byte * 81 = 81 bytes
    char email[41];      // 1 byte * 41 = 41 bytes
};

typedef struct aluno Aluno;

```


O número de dígitos efetivos na matrícula são 7, pois o último dígito é o de verificação (ou controle). Para permitir um acesso a qualquer aluno em ordem constante, podemos usar o número de matrícula do aluno como índice de um vetor. Um problema é que pagamos um preço alto para ter esse acesso rápido. Porque !? Resp: Visto que a matrícula é composta de 7 dígitos, então podemos esperar uma matrícula variando de 0000000 a 9999999. Portanto, precisaríamos dimensionar um vetor com DEZ Milhões de elementos.

Como a estrutura de cada aluno ocupa 126 bytes, então seriam necessários reservar 1.260.000.000 bytes, ou seja, acima de 1 GByte de memória. Como na prática teremos em torno de 50 alunos em uma turma cadastrados no curso, precisaríamos na realidade de 7.300 (=126*50) bytes. Pergunta: Como amenizar o gasto excessivo de memória!? Resp: Utilizando um vetor de ponteiros, em vez de um vetor de estruturas. Porque melhor vetor de ponteiros ? 
	- Alocação dos alunos cadastrados seria realizada dinamicamente.
	-  Portanto, considerando que cada ponteiro ocupa 4 bytes, o gasto excedente de memória seria 40.000.000 bytes. (~= 38 MBytes)

#### Alocação dinâmica?
	A alocação dinâmica é um conceito relacionado à manipulação de memória em linguagens de programação, como C ou C++. Alocar dinamicamente memória significa reservar espaço de memória durante a execução do programa, em vez de usar a alocação estática, que ocorre em tempo de compilação. A alocação dinâmica é útil quando você precisa criar ou manipular estruturas de dados de tamanho variável, como arrays ou estruturas, cujo tamanho pode ser determinado em tempo de execução.

Apesar da diminuição do gasto de memória, este gasto é considerável e desnecessário.
A forma de resolver o problema de gasto excessivo de memória, garantindo um acesso rápido, é através de Hashing. Pergunta: Como construir a Tabela Hash para armazenar as
informações dos alunos de uma determinada turma de um curso específico? resp: Identificando as partes significativas da chave.

Analisando a chave: Desconsiderando o último dígito (controle),
temos outros dígitos com significados especiais:

![[Pasted image 20230706224434.png]]

Portanto, podemos considerar no cálculo de endereço parte do número da matrícula.
Esta parte mostra a dimensão que a Tabela Hash deverá ter. Por exemplo, dimensionando com apenas 100 elementos, ou seja, Aluno* tabAlunos[100]. Pergunta: Qual a função que aplicada sobre matrículas de alunos retorna os índices da tabela? resp: Depende, qual é a turma e o curso específico dos alunos que devem ser armazenados ?

Supondo que a turma seja do 2º semestre de 2005 (código 052) e do curso de Sistemas de Informação (código 35). Qual seria a função de hashing perfeito !?

```
int funcao_hash(int matricula) {
	int valor = matricula – 0523500;
	if((valor >= 0) & (valor <=99)) {
			return valor;
	} else {
		return -1;
	}
}

// Acesso: dada mat  tabAlunos[funcao_hash(mat)]

```

Enfim, hashing perfeito é quando não ocorre colisões. Existem várias formas de alcançar um hashing perfeito:

- Tamanho da tabela hash igual ao número de chaves: 
	Nessa abordagem, o tamanho da tabela hash é definido para ser exatamente igual ao número de chaves a serem inseridas. Dessa forma, cada chave recebe um índice exclusivo e não há colisões. No entanto, essa abordagem pode resultar em desperdício de espaço se o número de chaves for pequeno em relação ao tamanho máximo da tabela;
- Funções hashing perfeitas:
	Uma função de hashing perfeita é uma função que mapeia cada chave para um índice exclusivo na tabela hash, sem colisões. Essas funções são geralmente mais complexas e exigem cálculos mais elaborados para garantir um mapeamento único. No entanto, encontrar funções de hashing perfeitas pode ser difícil e consome recursos computacionais;
- Hashing com encadeamento:
	Essa abordagem lida com colisões por meio do encadeamento. Em vez de mapear cada chave para um único índice, cada posição na tabela hash é uma lista vinculada (encadeada) de elementos com colisões. Dessa forma, diferentes chaves podem ser armazenadas na mesma posição da tabela. O encadeamento resolve as colisões e permite que a tabela hash acomode mais elementos do que o tamanho total da tabela;

OBS: A maioria das implementações de tabelas hash usa técnicas de tratamento de colisões, como encadeamento ou sondagem linear, para lidar com colisões de forma eficiente, mesmo que não seja um hashing perfeito
