
## Método da divisão

O método da divisão é uma técnica comumente utilizada em hashing para calcular o índice em uma tabela hash. Esse método envolve a divisão do valor da chave pelo tamanho da tabela hash e, em seguida, tomando o resto da divisão como o índice:

	h(x) = x % tableSize     (o tableSize é o tamanho do array)

Problema: Elementos distintos podem receber o mesmo índice, por exemplo, se tablesize é 10, e os elementos terminam todos em zero. Recomenda-se que o valor escolhido para
tablesize seja um número primo. Isso porque a escolha de tablesize influencia o espalhamento dos registros, e números primos tendem a distribuir os restos da divisão de maneira mais uniforme que os não primos.

Problema: se tablesize é muito grande a função não distribui bem os elementos. suponha tablesize = 10.007 (número primo) e que todas as strings possuam no máximo oito caracteres. Desde que o código ASCII de um caracter é no máximo 127 a função acima assumirá valores entre 0 e 1016, não gerando uma distribuição equilibrada

Se estivermos tratando de Strings, podemos quantificar pela tabela ASCII

```
private int h(String chave) {
    int hashval, j;
    // Inicializa o valor hash com o código ASCII do primeiro caractere da chave
    hashval = chave.charAt(0);  
    
    for (j = 1; j < chave.length(); j++) {
	    // Adiciona o código ASCII dos caracteres subsequentes à variável hashval
        hashval += chave.charAt(j);  
    }
        // Supondo que tablesize é uma variável global que representa o tamanho da tabela hash
        
    return (hashval % tablesize);  // Retorna o valor hash calculado, fazendo a operação de módulo pelo tamanho da tabela
}

```


## Método do hashing universal

- Qualquer função hash está sujeita ao problema de criar chaves iguais para elementos distintos.
- Dependendo da entrada, algumas funções hash podem espalhar os elementos de forma mais equilibrada que outras.
	se pudermos utilizar diferentes funções hash, teremos em média um espalhamento mais equilibrado.
- Uma estratégia que tenta minimizar o problema de colisões é o hashing universal.
- A ideia é escolher aleatoriamente (em tempo de execução) uma função hash a partir de um conjunto de funções cuidadosamente projetado.
- Um conjunto de funções pode ser gerado da seguinte forma:
	Suponha tablesize um número primo.
	Decomponha x em r+1 bytes (para o caso de strings, decompõe-se em caracteres ou
substrings). Seja p={p 0 , p 1 , …, p r } uma sequência de pesos
gerado randomicamente:

![[Pasted image 20230715120150.png]]

```
private int hu(String chave) {
    int hashval = 0;
    for (int i = 0; i < chave.length(); i++) {
        // Multiplica o valor numérico do caractere pelo peso correspondente
        // na posição 'i' do array 'pesos' e adiciona ao 'hashval'
        hashval += chave.charAt(i) * pesos[i];
    }
    // Aplica a operação de módulo 'tablesize' para garantir que o valor hash
    // esteja dentro do intervalo desejado
    return hashval % tablesize;
}

private int[] geraPesos(int n) {
    Random rnd = new Random();
    int p[] = new int[n];
    for (int i = 0; i < n; i++) {
        // Gera um número aleatório e aplica a operação de módulo 'tablesize'
        // para limitar o valor dentro do intervalo desejado
        // Adiciona 1 ao resultado para evitar que o peso seja zero
        p[i] = (rnd.nextInt(Integer.MAX_VALUE) % tablesize) + 1;
    }
    return p;
}

```


## Considerações sobre funções de hashing

* Na prática funções de hashing perfeitas ou quase perfeitas:
	* são encontradas apenas onde a colisão não é tolerável (nas funções de hashing na criptografia);
	* Quando conhecemos previamente o conteúdo a ser armazenado na tabela.

* Nas Tabelas Hash comuns a colisão é apenas indesejável, diminuindo o desempenho do sistema.
* Para resolver os problemas de colisão em Tabelas Hash, é comum combinar essas estruturas de dados adicionais, como:
	- Listas Encadeadas: Ao encontrar uma colisão, os elementos com chaves hash iguais são armazenados em uma lista encadeada dentro da tabela hash. Isso permite lidar com várias entradas com a mesma chave hash, mantendo uma sequência linear de elementos relacionados.
    
	- Árvores Balanceadas: Em vez de usar listas encadeadas, uma estrutura de árvore balanceada, como uma árvore binária de busca (BST) ou uma árvore rubro-negra, pode ser usada para armazenar os elementos colididos. Essas estruturas de árvore oferecem tempos de busca eficientes e podem melhorar o desempenho quando há muitas colisões.
    
	- Dentro da própria tabela: Em alguns casos, a própria tabela hash pode ser expandida para acomodar múltiplos valores associados a uma mesma chave hash. Isso pode ser feito usando estratégias como encadeamento separado ou endereçamento aberto, onde cada entrada da tabela pode armazenar mais de um valor.
    
	Essas estruturas de dados auxiliares ajudam a resolver os problemas de colisão que podem ocorrer em Tabelas Hash, permitindo o armazenamento eficiente e recuperação de elementos, mesmo quando há várias chaves que resultam na mesma posição da tabela hash.