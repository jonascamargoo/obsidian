
estrutura do algoritmo genético

1 - inicialização da população
	deve ser inicializado com valores aleatórios
	devemos explorar o maior número possível de populção, explorar o máximo global

2 - avaliação de cada indivíduo
	avaliação feita pela fitness function
	
3 - seleção de alguns indivíduos
	é importante selecionar não apenas os melhores indivíduos para diversificar as soluções e evitar máximos locais
	temos a seleção proporcional ao fitness, onde os indivíduos tem chance de serem escolhidos proporcionalmente ao seu fitness value.e temos também a seleção proporcional ao ranking, onde os indivíduos tem chance de serem escolhidos proporcionalmente ao seu ranking dentre os indivíduos
	
4 - cross-over e mutação
	
5 - concepção da nova geração
6 - repita até estar satisfeito com as soluções
7 - fim do algoritmo