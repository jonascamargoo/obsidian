## **Ideia básica**

cada programa possui seu próprio **espaço de endereçamento**, dividido em blocos chamados **páginas**. As **páginas** correspondem a partes do espaço de **memória virtual** que são mapeadas para quadros (frames) na **memória física**. Essas páginas são mapeadas na memória física, mas nem todas precisam estar carregadas simultaneamente para que o programa seja executado.  
Quando o programa acessa uma parte do espaço de endereçamento que está na memória física, o hardware realiza rapidamente o mapeamento necessário. Caso o programa tente acessar uma parte que não está carregada, o sistema operacional é alertado para buscar a página ausente e reexecutar a instrução que falhou.

Geralmente, os frames e as páginas possuem o mesmo tamanho, porém quadros não são contíguos. Com isso, o que é um endereço contíguo na memória, pode está completamente embaralhado no frame (quadro de página). Chamamos isso de [Realocação](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FComputer%20Organization%20and%20Architecture%2FHierarquia%20de%20mem%C3%B3ria%2Fvirtual%20memory). OBS: isso inclui a tabela de páginas, que também está com seus pedaços embaralhados se olharmos pela perspectiva da memória física.

### **Memória Virtual como Generalização de Registradores Base e Limite**

A memória virtual pode ser vista como uma **extensão do conceito de registradores base e limite** (utilizados para delimitar o início e fim do espaço de endereçamento). Por exemplo, o processador 8088 utilizava registradores base separados (mas sem registradores limite) para segmentos de texto e dados. Com a introdução da memória virtual, o sistema permite que o espaço de endereçamento completo seja mapeado na memória física em unidades menores e mais gerenciáveis, indo além da segmentação básica. Isso torna o processo de realocação mais flexível e eficiente, abrangendo todo o espaço de endereçamento. Transferências entre a memória RAM e o disco são sempre em páginas inteiras, mas, por exemplo, uma arquitetura x86-64 dá suporte a páginas de 4 KB, 2 MB e 1 GB, então poderíamos usar páginas de 4 KB para aplicações do usuário e uma única página de 1 GB para o núcleo.


### **Memória Virtual em Sistemas de Multiprogramação**

A memória virtual é especialmente eficaz em sistemas de **multiprogramação**, onde pedaços de vários programas podem coexistir na memória ao mesmo tempo. Enquanto um programa aguarda o carregamento de partes de si mesmo, a CPU pode ser alocada para outro processo, maximizando a utilização dos recursos. Essa abordagem garante uma execução mais eficiente e permite o suporte a múltiplos programas sem a necessidade de carregar completamente todos eles na memória.

## Problemas resolvidos pela memória virtual

Memórias virtuais atacam três problemas

### Key Problem

O problema chave é a possibilidade de dois processos acessarem o mesmo endereço de memória ao mesmo tempo. Como resolver? Dando a um processo seu próprio bloco de endereços, chamado de memória virtual, com seu endereço virtual. Esses espaços são chamados páginas. Alguns problemas secundários são:

### Not enough memory

O CPU demanda naturalmente mais espaço do que a memória possui

![[Pasted image 20250115132042.png]]

#### Solution

Com a memória virtual, conseguimos fazer com que cada processo tenha um espaço de endereçamento virtual (chamados páginas), correspondente (mapeado) à memória física, tendo mais dados disponíveis, fazendo a troca necessária (princípio da localidade espacial e temporal). 

Para visualizar melhor, temos um exemplo prático. Nesse exemplo, temos um computador que gera endereços de 16 bits, de 0 a 64 K − 1. Esses são endereços virtuais. Esse computador, no entanto, tem apenas 32 KB de memória física. Então, embora programas de 64 KB possam ser escritos, eles não podem ser totalmente carregados na memória e executados. Uma cópia completa da imagem de núcleo de um programa, de até 64 KB, deve estar presente no disco, entretanto, de maneira que partes possam ser carregadas quando necessário:

![[Pasted image 20250115150145.png]]


Visualizando o processo ponta a ponta:

![[Pasted image 20250115133712.png]]

![[Pasted image 20250115133810.png]]

### Memory Fragmentation

Espaços livres espalhados

![[Pasted image 20250115132445.png]]

#### Solution

Com a memória virtual, é possível mapear para os endereços livres

![[Pasted image 20250115134001.png]]
### Security

Possibilidade de corromper os dados de outro programa

![[Pasted image 20250115132659.png]]


#### Solution

A primeira parte a ser solucionada pela memória virtual é que agora, mesmo que os processos acessem o mesmo endereço, eles iram acessar o endereço virtual e não o físico.

![[Pasted image 20250115134844.png]]


Outro ponto é o **Sharing Data**. No caso de uma biblioteca que precisa ser compartilhada, como uma biblioteca dinâmica (shared library), o sistema operacional pode mapear a mesma página de memória física (frame) para os espaços de endereçamento de ambos os programas. Isso permite que ambos os programas acessem a biblioteca sem duplicar seu conteúdo na memória física, economizando recursos.

![[Pasted image 20250115135531.png]]

## Mapping - Page Table

O mapeamento de endereços virtuais para endereços físicos divide o endereço virtual em duas partes: número da página virtual (bits superiores) e deslocamento (bits inferiores). Por exemplo, com um endereço de 16 bits e páginas de 4 KB, 4 bits superiores identificam uma das 16 páginas, enquanto 12 bits inferiores indicam o deslocamento dentro da página.

O número da página virtual é usado como índice na tabela de páginas para localizar o número do quadro correspondente. Este quadro substitui o número da página virtual, formando o endereço físico final. Assim, a tabela de páginas atua como uma função que mapeia páginas virtuais para quadros físicos.

Cada entrada na tabela de páginas contém informações como:

- **Bit Presente/Ausente**: Indica se a página está na memória. Um valor 0 causa uma falta de página.
- **Bits de Proteção**: Determinam permissões de acesso (leitura, escrita, execução).
- **Bits Modificada e Referenciada**: Controlam o uso da página, auxiliando na substituição em caso de falta de páginas.
- **Bit de Cache**: Permite desabilitar o cache para páginas que mapeiam dispositivos de E/S.

A tabela de páginas armazena informações necessárias para o hardware traduzir endereços virtuais em físicos, enquanto dados para lidar com faltas de páginas são mantidos em tabelas de software pelo sistema operacional.

A memória virtual é uma abstração que gerencia o espaço de endereçamento, dividindo-o em páginas e mapeando-as para quadros de memória física. Isso possibilita o gerenciamento eficiente de memória pelo sistema operacional.



![[Pasted image 20250115170417.png]]

![[Pasted image 20250115170629.png]]