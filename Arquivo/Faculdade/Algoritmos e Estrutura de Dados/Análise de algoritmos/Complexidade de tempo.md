---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

#### Dois if's ou if/else?

Em termos de desempenho, a diferença é insignificante. A JVM (Java Virtual Machine) é otimizada para realizar branch prediction (previsão de ramificação) e outras otimizações de código, tornando a diferença de desempenho negligível.

### Código e suas respectivas funções

void funcao(int a, int n) {

	for (int i=1; i < 3; i++)
		for (int j=i; j < n+1; j++)
			for (int k=i; k < j+1; k++)
				if (a % 2 == 0)
					a = a + i + j + k;

}

int funcao(int n) {

	if (n == 0)
		return(1);
	else
		return(funcao(n-1)+funcao(n-1));

}

	a relação de recorrência desse algoritmo é:
	T(n) = 2T(n-1)
	T(0) = 1

void funcao(int n) {

	if (n > 1) {
		// Divide n em 3 partes iguais
		// n1, n2, n3 com custo de n*n
		// passos;
		funcao(n1);
		funcao(n2);
		funcao(n3);
	}
}

	T(n) = 3T(n/3) + n² + 1
	//esse +1 é do if



void pesquisa(int n) {

	if (n > 1) {
	// Inspecione n*n*n elementos;
	pesquisa(2n/3);

}

	T(n) = T(2n/3) + n² + 1