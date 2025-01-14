memórias virtuais atacam três problemas:

1) not enough memory
2) memory fragmentation
3) Security

## **Ideia básica**

cada programa possui seu próprio **espaço de endereçamento**, dividido em blocos chamados **páginas**, que são séries contíguas de endereços. Essas páginas são mapeadas na memória física, mas nem todas precisam estar carregadas simultaneamente para que o programa seja executado.  
Quando o programa acessa uma parte do espaço de endereçamento que está na memória física, o hardware realiza rapidamente o mapeamento necessário. Caso o programa tente acessar uma parte que não está carregada, o sistema operacional é alertado para buscar a página ausente e reexecutar a instrução que falhou.


### **Memória Virtual como Generalização de Registradores Base e Limite**

A memória virtual pode ser vista como uma **extensão do conceito de registradores base e limite** (utilizados para delimitar o início e fim do espaço de endereçamento). Por exemplo, o processador 8088 utilizava registradores base separados (mas sem registradores limite) para segmentos de texto e dados. Com a introdução da memória virtual, o sistema permite que o espaço de endereçamento completo seja mapeado na memória física em unidades menores e mais gerenciáveis, indo além da segmentação básica. Isso torna o processo de realocação mais flexível e eficiente, abrangendo todo o espaço de endereçamento.


### **Memória Virtual em Sistemas de Multiprogramação**

A memória virtual é especialmente eficaz em sistemas de **multiprogramação**, onde pedaços de vários programas podem coexistir na memória ao mesmo tempo. Enquanto um programa aguarda o carregamento de partes de si mesmo, a CPU pode ser alocada para outro processo, maximizando a utilização dos recursos. Essa abordagem garante uma execução mais eficiente e permite o suporte a múltiplos programas sem a necessidade de carregar completamente todos eles na memória.


OBS: a repartição é tanta que a própria tabela é separada! (bruno falou)!!!!!!!!!