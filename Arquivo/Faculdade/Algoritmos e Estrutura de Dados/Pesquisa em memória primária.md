
	Pesquisas em memória primária referem-se a operações de busca e acesso a dados armazenados na memória principal de um computador. A memória principal, também conhecida como memória RAM (Random Access Memory), é um tipo de memória de acesso aleatório e volátil, que é utilizada para armazenar dados temporariamente enquanto um programa está em execução.

	As pesquisas em memória primária são comumente realizadas para localizar e recuperar informações específicas armazenadas na memória, seja por um programa em execução ou por um sistema operacional. Essas pesquisas podem ser realizadas utilizando diferentes técnicas e algoritmos, dependendo das necessidades e características do sistema.

	- A informação é dividida em registros, cada registro possui uma chave para ser usada na pesquisa

	- Objetivo da pesquisa: Encontrar uma ou mais ocorrências de registros com chaves iguais à chave de pesquisa


#### Tabelas

	-  Conjunto de registros ou arquivos são armazenados em tabelas
	-  Tabela: associada a entidades de vida curta, criadas na memória interna durante a execução de um programa. Ou seja, dados temporários que são criados e usados ​​durante a execução de um programa. Essas tabelas são armazenadas na memória interna do sistema e podem ser manipuladas rapidamente para realizar operações como filtragem, cálculos ou análises temporárias.
	
	-  Arquivo: geralmente associado a entidades de vida mais longa, armazenadas em memória externa. Ou seja, dados que são armazenados de forma persistente em memória externa, como em discos rígidos ou outros dispositivos de armazenamento. Esses arquivos são criados para armazenar dados permanentes que podem ser acessados mesmo após a execução de um programa.
	
	- Distinção não é rígida: existem casos em que as características se sobrepõem
		- tabela: arquivo de índices Uma tabela pode ser usada como um arquivo de índices, onde os registros são organizados para permitir um acesso mais eficiente aos dados em outros arquivos relacionados. Os índices podem ser usados para acelerar a busca e a recuperação de informações em um banco de dados.
		- arquivo: tabela de valores de funções: Um arquivo pode ser usado como uma tabela de valores de funções, onde os registros representam valores de entrada e saída de uma função específica. Esses arquivos podem ser usados para consulta rápida de valores de função pré-calculados sem a necessidade de executar novamente o cálculo da função.

##### Escolha do Método de Pesquisa mais Adequado a uma Determinada Aplicação

	- Depende principalmente:
		-  Quantidade dos dados envolvidos.
		- Arquivo estar sujeito a inserções e retiradas frequentes.

	-  Se conteúdo do arquivo é estável é importante minimizar o tempo de pesquisa, sem preocupação com o tempo necessário para estruturar o arquivo

##### Algoritmos de Pesquisa Tipos Abstratos de Dados

	- É importante considerar os algoritmos de pesquisa como tipos abstratos de dados (TADs), com um conjunto de operações associado a uma estrutura de dados, de tal forma que haja uma independência de implementação para as operações.
	- Operações mais comuns:
	-  Inicializar a estrutura de dados.
	-  Pesquisar um ou mais registros com determinada chave.
	-  Inserir um novo registro.
	- Retirar um registro específico.
	- Ordenar um arquivo para obter todos os registros em ordem de acordo com a chave.
	-  Juntar dois arquivos para formar um arquivo maior.

#### Dicionário

	- Nome comumente utilizado para descrever uma estrutura de dados para pesquisa.
	- Dicionário é um tipo abstrato de dados com as operações:
		1. Inicializa
		2. Pesquisa
		3. Insere
		4. Retira

	- No contexto de dicionários no armazenamento de dados, as afirmações estão estabelecendo uma analogia com um dicionário da língua portuguesa. Vamos entender o significado de cada afirmação:
		1. Chaves ↔ palavras: Nessa analogia, as chaves são equivalentes às palavras. Assim como em um dicionário tradicional, onde cada palavra é associada a uma definição, no contexto de dicionários de armazenamento de dados, as chaves são usadas para identificar e acessar os registros correspondentes.
		2. Registros ↔ entradas associadas com *pronúncia, definição, sinônimos, outras informações: Aqui, os registros são comparados a entradas de um dicionário que contêm informações associadas a uma palavra. Essas informações podem incluir a pronúncia, definição, sinônimos e outras informações relevantes sobre a palavra
		No contexto de armazenamento de dados, um registro pode ser uma estrutura que contém várias informações relacionadas a um determinado item ou conceito. Por exemplo, em um dicionário de dados que armazena informações sobre produtos, um registro pode conter detalhes como o nome do produto, descrição, preço, categoria, entre outros atributos. É importante destacar que a utilização de dicionários como estruturas de dados pode variar dependendo da tecnologia ou linguagem de programação utilizada.

#### Tad tabela
```
public class Tabela {
    private Item registros[];
    private int n;
    
    public Tabela(int maxN) {
        this.registros = new Item[maxN + 1];
        this.n = 0;
    }
    
    public int pesquisa(Item reg) {...}
    
    public void insere(Item reg) throws Exception {
        if (this.n == (this.registros.length - 1))
            throw new Exception("Erro: A tabela está cheia");
        this.registros[++this.n] = reg;
    }
    
    public int binaria(Item chave) {...}
}

```

## Tipos de pesquisa em memória primária

### -> Pesquisa Sequencial
	- Nessa abordagem, os dados são acessados em uma sequência linear, um após o outro, a partir do primeiro registro, até que a chave desejada seja encontrada. É uma técnica simples, porém pode ser ineficiente para grandes conjuntos de dados.

##### Armazenamento de um conjunto de registros por meio do tipo estruturado arranjo:

```
public int pesquisa (Item reg) {
	this.registros[0] = reg; // @{\it sentinela}@
	int i = this.n;
	while (this.registros[i].compara (reg) != 0)
		i--;
		return i;
	}
}
```

	- Pesquisa retorna o índice do registro que contém a chave x;
	- Caso não esteja presente, o valor retornado é zero.
	- A implementação não suporta mais de um registro com uma mesma chave.
	- Para aplicações com esta característica é necessário incluir um argumento a mais na função Pesquisa para conter o índice a partir do qual se quer pesquisar.
	- Utilização de um registro sentinela na posição zero
	do array:
		-  Garante que a pesquisa sempre termina: se o índice retornado por Pesquisa for zero, a pesquisa foi sem sucesso.
		-  Não é necessário testar se i > 0, devido a isto:
		- o anel interno da função Pesquisa é extremamente simples: o índice i é decrementado e a chave de pesquisa é comparada com a chave que está no registro.
		- isto faz com que esta técnica seja conhecida como pesquisa sequencial rápida.


#### Análise
	-  Pesquisa com sucesso:
		melhor caso : C(n) = 1
		pior caso : C(n) = n
		caso médio: C(n) = (n + 1) / 2

	- Pesquisa sem sucesso:
		- C (n) = n + 1

	O algoritmo de pesquisa sequencial é a melhor escolha para o problema de pesquisa em tabelas com até 25 registros






### -> Pesquisa Binária

- Pesquisa em tabela pode ser mais eficiente se registros forem mantidos em ordem
- Para saber se uma chave está presente na tabela
	1. Compare a chave com o registro que está na posição do meio da tabela.
	2. Se a chave é menor então o registro procurado está na primeira metade da tabela
	3. Se a chave é maior então o registro procurado está na segunda metade da tabela.
	4. Repita o processo até que a chave seja encontrada, ou fique apenas um registro cuja chave é diferente da procurada, significando uma pesquisa sem sucesso

```
public int binaria(Item chave) {
    if (this.n == 0)
        return 0;
    int esq = 1, dir = this.n, i;
    do {
        i = (esq + dir) / 2;
        if (chave.compara(this.registros[i]) > 0)
            esq = i + 1;
        else
            dir = i - 1;
    } while ((chave.compara(this.registros[i]) != 0) && (esq <= dir));
    
    if (chave.compara(this.registros[i]) == 0)
        return i;
    else
        return 0;
}

```

#### Análise

- A cada iteração do algoritmo, o tamanho da tabela é dividido ao meio.
- Logo: o número de vezes que o tamanho da tabela é dividido ao meio é cerca de log n.
- Ressalva: o custo para manter a tabela ordenada é alto: a cada inserção na posição p da tabela implica no deslocamento dos registros a partir da posição p para as posições seguintes.
- Consequentemente, a pesquisa binária não deve ser usada em aplicações muito dinâmicas.