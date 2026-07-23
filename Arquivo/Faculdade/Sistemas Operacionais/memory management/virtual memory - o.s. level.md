---
tipo: conceito
area: Sistemas Operacionais
tags:
- so
criada: '2025-01-14'
---

## **Ideia básica**

cada programa possui seu próprio **espaço de endereçamento**, dividido em blocos chamados **páginas**. As **páginas** correspondem a partes do espaço de **memória virtual** que são mapeadas para quadros (frames) na **memória física**. Essas páginas são mapeadas na memória física, mas nem todas precisam estar carregadas simultaneamente para que o programa seja executado.  
Quando o programa acessa uma parte do espaço de endereçamento que está na memória física, o hardware realiza rapidamente o mapeamento necessário. Caso o programa tente acessar uma parte que não está carregada, o sistema operacional é alertado para buscar a página ausente e reexecutar a instrução que falhou.

Geralmente, os frames e as páginas possuem o mesmo tamanho, porém quadros não são contíguos. Com isso, o que é um endereço contíguo na memória, pode está completamente embaralhado no frame (quadro de página). Chamamos isso de [[virtual memory - low level|Realocação]]. OBS: isso inclui a tabela de páginas, que também está com seus pedaços embaralhados se olharmos pela perspectiva da memória física.
## Resumo
### Conceito e Funcionamento  

Cada processo possui seu próprio espaço de endereçamento na memória virtual. Esse espaço de endereçamento virtual é mapeado para endereços correspondentes na memória física. Isso resolve o problema de falta de espaço na RAM, pois, se ao mapear o endereço virtual para o físico o dado não for encontrado na RAM, ele pode ser buscado em níveis inferiores de memória (como o disco, por meio de swap in/swap out).

Outro problema resolvido é a fragmentação de memória. Como os endereços virtuais não precisam ser alocados de forma contígua na memória física, cada chunk (ou página) é mapeado de forma embaralhada. Isso também inclui a própria page table. Além disso, a memória virtual aumenta a segurança e evita race conditions. Isso ocorre porque, se mais de um programa tentar acessar um endereço virtual igual, esses endereços serão mapeados para locais distintos na memória física, isolando os processos.

### Mapeamento e Page Table

Um mapeamento entre endereços virtuais e físicos é chamado de page table entry (PTE). Para cada endereço virtual, existe uma entrada correspondente na page table, que é armazenada na RAM.

### Page Fault 

Durante um page fault, o CPU verifica se o endereço virtual acessado contém dados do processo atual. Se sim, os dados podem ser movidos do disco rígido (hard disk) para a RAM e, então, alocados no endereço físico correspondente. Caso contrário, a página requisitada apenas sobrescreve outra, conforme a política de substituição de páginas.

### Problema de Acesso

O uso de page tables adiciona sobrecarga: para cada acesso a um endereço virtual, é necessário:

1. Localizar a entrada correspondente na page table (1 acesso à RAM);
    
2. Obter o endereço físico correspondente (outro acesso à RAM).
    

Isso significa que cada tradução exige pelo menos dois acessos à RAM. Para mitigar esse problema, utilizamos o TLB (Translation Lookaside Buffer).

### TLB: Tradução Rápida  

O TLB é um tipo de cache que armazena traduções recentes entre endereços virtuais e físicos. Apesar de ser pequeno, o TLB é muito eficiente devido ao princípio de localidade espacial. Existem dois tipos principais de TLB:

- ITLB: usado para instruções.
    
- DTLB: usado para dados.
    

O TLB permite que a busca por traduções seja realizada em menos de 1 ciclo de clock, tornando o acesso muito rápido. Se o endereço virtual não estiver no TLB (miss), a tradução será feita utilizando a page table. Após a tradução, a MMU armazena o resultado no TLB para futuros acessos. Observação  A "tradução" mencionada é o conteúdo armazenado na page table, composto por uma coluna com os endereços virtuais e outra com os endereços físicos correspondentes. O uso direto da page table é uma exceção, ocorrendo apenas em caso de TLB miss.

### Endereço limite
O número de páginas na memória física é determinado pelo tamanho da RAM. Já o espaço de endereçamento virtual (e o tamanho máximo da page table) é limitado pela arquitetura do sistema. Por exemplo, uma arquitetura de 32 bits limita a memória endereçável a 4 GiB, mesmo que a RAM física seja maior, como 64 GiB. Esse limite é intrínseco ao tamanho dos registradores da CPU.

### O que é atribuição do CPU e o que é da MMU?
#### CPU

Gera o endereço virtual a partir de instruções e dados do programa. Consulta o TLB para verificar se a tradução está disponível. Em caso de page fault, aciona o sistema operacional para buscar os dados no disco. 

### MMU (Memory Management Unit)

Realiza a tradução do endereço virtual para o físico. Armazena traduções no TLB após consultá-las na page table. Controla o acesso à memória física, garantindo isolamento entre os processos.

### O que é o offset na memória virtual?

O offset é a parte do endereço que indica uma posição específica dentro de uma página. Uma página é um bloco fixo de memória (normalmente 4 KiB). O endereço virtual é dividido em duas partes principais:

1. Número da página virtual (VPN - Virtual Page Number): Indica qual página (bloco) o dado pertence.
    
2. Offset: Indica onde, dentro da página, o dado específico está localizado.
    

---

### Como o offset funciona na tradução para o endereço físico?

1. O endereço virtual gerado pelo programa é dividido em duas partes:
    

- Os bits mais significativos indicam o número da página virtual.
    
- Os bits menos significativos (o offset) indicam a posição exata dentro dessa página.
    

3. A MMU (Unidade de Gerenciamento de Memória) usa a página virtual (VPN) para localizar a entrada correspondente na page table, que armazena a tradução para a página física.
    
4. A página física, combinada com o mesmo offset do endereço virtual, forma o endereço físico final.
    

---

### Exemplo com 4 KiB por página

Se a página tem 4 KiB (2¹² bytes), o offset precisa de 12 bits para endereçar qualquer posição dentro dessa página. O endereço virtual completo pode ser, por exemplo, de 32 bits. Assim:

- Bits do endereço virtual:
    

- 20 bits para o número da página virtual (VPN).
    
- 12 bits para o offset (posição dentro da página).
    

Tradução na prática:

1. Digamos que o endereço virtual seja 0x12345AB0 (em hexadecimal, ou 32 bits).
    
2. Em binário:
    

- 0001 0010 0011 0100 0101 1010 1011 0000
    

4. Dividimos em:
    

- VPN: 0001 0010 0011 0100 0101 (os 20 bits mais significativos).
    
- Offset: 1010 1011 0000 (os 12 bits menos significativos).
    

6. A MMU usa a VPN para buscar na page table qual página física corresponde a essa página virtual.
    

- Suponha que a página virtual 0x12345 (VPN) está mapeada para a página física 0x3A7.
    

8. A MMU combina a página física (0x3A7) com o offset (0xAB0) para formar o endereço físico final:
    

- Endereço físico = 0x3A7AB0.
    


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