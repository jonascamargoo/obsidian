---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware
criada: '2024-10-14'
---

"A technique that uses main memory as a “cache” for secondary storage." Uma espaço (swap space) de disco rídigo utilizado como se fosse parte da memória principal

### Para que? 

![[Pasted image 20231117184109.png]]


### Conceitos chave:

- Memória física (physical address) ->An address in main memory;
- page fault -> An event that occurs when an accessed page is not present in main memory;
- virtual address -> An address that corresponds to a location in virtual space and is translated by address mapping to a physical address when memory is accessed;
- address translation -> Also called address mapping. The process by which a virtual address is mapped to an address used to access memory.
- Processo vs programa -> O "processo" refere-se à instância em execução de um programa, incluindo seu estado atual, enquanto o "programa" se refere ao conjunto de instruções e dados que compõem a lógica do software.

### Realocação

A realocação mapeia os endereços virtuais usados por um programa para diferentes endereços físicos antes que esses endereços sejam utilizados para acessar a memória. Esse processo de realocação permite carregar o programa em qualquer lugar da memória principal. Isso elimina a necessidade de encontrar um bloco contínuo de memória para alocar para um programa. Em vez disso, o sistema operacional só precisa encontrar um número suficiente de páginas livres na memória principal. Esse método simplifica a gestão da memória, pois não é mais necessário encontrar uma grande área contígua para alocar um programa, facilitando a alocação de espaço na memória principal -> Ou seja, pode haver um processo (programa) A, processo B e processo A, todos eles rodando inconscientes da existência um do outro.

### Placing a Page and Finding it Again

Devido à penalidade significativamente alta para uma falha de página, os projetistas buscam reduzir a frequência dessas falhas otimizando o posicionamento das páginas. Ao permitir que uma página virtual seja associada a qualquer página física, o sistema operacional pode escolher substituir qualquer página durante uma falha de página. Isso permite o uso de algoritmos sofisticados e estruturas de dados complexas para selecionar páginas que provavelmente não serão necessárias por um longo tempo. A capacidade de empregar um esquema de substituição inteligente e flexível reduz a taxa de falhas de página e simplifica o uso de posicionamento totalmente associativo de páginas.
### Page tables

"The table containing the virtual to physical address translations in a virtual memory system. The table, which is stored in memory, is typically indexed by the virtual page number; each entry in the table contains the physical page number for that virtual page if the page is currently in memory."

Cada programa possui sua própria page table, que mapeia o espaço de endereçamento virtual desse programa para a memória principal. Em nossa analogia com uma biblioteca, a tabela de páginas corresponde a um mapeamento entre títulos de livros e localizações na biblioteca - pode ser que não esteja (page fault).

A page table, juntamente com o PC counter e os registradores, especifica o estado de uma VM. Para permitir que outra VM use o processador, é necessário salvar esse estado. Posteriormente, após a restauração desse estado, a VM pode retomar a execução. Este estado é frequentemente chamado de "processo". O processo é considerado ativo quando está em posse do processador; caso contrário, é considerado inativo. O sistema operacional pode tornar um processo ativo carregando o estado do processo, incluindo o contador de programa, que iniciará a execução no valor do contador de programa salvo.

O espaço de endereçamento do processo e, portanto, todos os dados aos quais ele pode acessar na memória, são definidos por sua tabela de páginas, que reside na memória. Em vez de salvar toda a tabela de páginas, o sistema operacional simplesmente carrega o registrador de tabela de páginas para apontar para a tabela de páginas do processo que deseja tornar ativo. Cada processo tem sua própria tabela de páginas, já que diferentes processos usam os mesmos endereços virtuais. O sistema operacional é responsável por alocar a memória física e atualizar as tabelas de páginas, para que os espaços de endereçamento virtual de diferentes processos não entrem em conflito. O uso de page tables separadas também proporciona proteção de um processo contra outro.


Vejamos esse exemplo ilustrativo:


![[Pasted image 20231117232547.png]]

"uses the page table register, the virtual address, and the indicated page table to show how the hardware can form a physical address. A valid bit is used in each page table entry, just as we did in a cache. If the bit is off, the page is not present in main memory and a page fault occurs. If the bit is on, the page is in memory and the entry contains the physical page number.


como a tabela de páginas contém um mapeamento para cada possível página virtual, não são necessárias etiquetas (tags). Em terminologia de cache, o índice usado para acessar a tabela de páginas consiste no endereço completo do bloco, que é o número da página virtual. o número da página virtual serve como índice direto para acessar a tabela de páginas, eliminando a necessidade de tags adicionais.

#### Como funciona?

### 1. **Divisão do Endereço Virtual**

O endereço virtual (gerado pelo programa em execução) é dividido em:

- **Número da Página Virtual**: Indica qual página virtual está sendo acessada. Corresponde aos bits mais significativos do endereço.
- **Deslocamento**: Determina a posição específica dentro da página virtual selecionada. Corresponde aos bits menos significativos do endereço.

Por exemplo:

- Um endereço de **16 bits**:
    - Se o tamanho da página for **4 KB (4096 bytes)**, serão necessários **12 bits** para o deslocamento, já que 212=40962^{12} = 4096212=4096.
    - Os **4 bits superiores** representam o número da página virtual (com 24=162^4 = 1624=16 páginas virtuais possíveis).

A divisão entre número de página e deslocamento depende diretamente do tamanho da página. Abaixo, uma operação interna na MMU com 16 páginas de 4 KB:

![[Pasted image 20250121142503.png]]

---

### 2. **Mapeamento com a Tabela de Páginas**

A tabela de páginas atua como uma função de tradução:

- O **número da página virtual** é usado como índice para acessar a tabela de páginas.
- A tabela armazena a correspondência entre números de páginas virtuais e **números de quadros de páginas** (frames), que são as unidades físicas na memória principal.

Se uma página virtual está **mapeada** na memória física, a entrada correspondente na tabela fornecerá o número do quadro físico.

---

### 3. **Construção do Endereço Físico**

Após encontrar o número do quadro físico:

1. Substituímos o número da página virtual pelo número do quadro físico.
2. O **deslocamento** é mantido inalterado.
3. A combinação desses valores forma o endereço físico.

---

### Exemplo:

- Tamanho da página: **4 KB**.
- Endereço virtual: **0xABCD (hexadecimal)**.
    - Número da página virtual: **A (4 bits)**.
    - Deslocamento: **BCD (12 bits)**.

Se a página virtual **A** está mapeada no quadro físico **7**, o endereço físico seria:

- Número do quadro físico: **7**.
- Deslocamento: **BCD**.
- Endereço físico: **0x7BCD**.

---

### 4. **Função da Tabela de Páginas**

Matematicamente, a tabela de páginas pode ser descrita como uma função fff, onde: f(Nuˊmero da Paˊgina Virtual)=Nuˊmero do Quadro Fıˊsicof(\text{Número da Página Virtual}) = \text{Número do Quadro Físico}f(Nuˊmero da Paˊgina Virtual)=Nuˊmero do Quadro Fıˊsico

Se o número da página virtual não estiver mapeado (ou seja, não existir no momento na memória física), ocorre uma **falha de página** (_page fault_), exigindo que o sistema operacional traga a página da memória secundária (disco).


### Page Faults

"If the valid bit for a virtual page is off, a page fault occurs. The operating system must be given control. This transfer is done with the exception mechanism. Once the operating system gets control, it must find the page in the next level of the hierarchy (usually flash memory or magnetic disk) and decide where to place the requested page in main memory."

##### Onde exatamente se encontra a página no disco?

O endereço virtual sozinho não nos diz imediatamente onde a página está no disco. Voltando à nossa analogia com uma biblioteca, não podemos encontrar a localização de um livro nas prateleiras apenas conhecendo o título. Em vez disso, consultamos o catálogo e procuramos o livro, obtendo um endereço para a localização nas prateleiras. Da mesma forma, em um sistema de memória virtual, precisamos acompanhar a localização no disco de cada página no espaço de endereço virtual.

Como não sabemos antecipadamente quando uma página na memória será substituída, o sistema operacional geralmente cria o espaço em memória flash ou disco para todas as páginas de um processo quando cria o processo. Esse espaço é chamado de espaço de troca (swap space). Nesse momento, também é criada uma estrutura de dados para registrar onde cada página virtual está armazenada no disco. Essa estrutura de dados pode ser parte da tabela de páginas ou pode ser uma estrutura de dados auxiliar indexada da mesma forma que a tabela de páginas.

##### Swap space

Como não podemos prever quando uma página na memória será substituída, o sistema operacional toma precauções. Quando um processo é criado, o sistema operacional reserva espaço em memória flash ou em disco para todas as páginas desse processo. Esse espaço é chamado de "swap space" (espaço de troca).


![[Pasted image 20231117235128.png]]


#### Tamanhos

Com um endereço virtual de 32 bits, páginas de 4 KiB e 4 bytes por tabela de páginas entrada, podemos calcular o tamanho total da tabela de páginas, seguindo a penúltima imagem:

32 bits ao todo para o endereço, 12 desses são offset de página

$$\text{pageTableEntries} = \frac{2^{32}}{2^{12}} = 2^{20}$$

Dado que cada entrada na tabela de páginas tem 4 bytes, o tamanho da entrada da tabela de páginas é 4 bytes:

$$ \text{sizeOfPageTable} = 2^{20} \times 4 \, \text{bytes} = 4 \, \text{MiB} \ $$


#### TLB: making Address Translation Fast

Como as page tables estão na memória principal, todo acesso à memória por um programa custaria dois acessos: um para obter o endereço físico e outro para ler ou escrever o dado. Para evitar isso, explora-se o princípio da localidade, com um cache especial: *translation-lookaside buffer (TLB)*  - cache that keeps track of recently used address mappings to try to avoid an access to the page table. Ou seja, uma cache que armazena a tradução de virtual para físico. Geralmente é um componente de hardware, cache fully-associative.

![[Pasted image 20231126081858.png]]

##### Dígitos do endereçamento

###### Page table
| validade | dirty | ref | endereço físico |

bit validade: se for 1 -> página residente na memória principal ; se for 2 -> está apenas no disco

bit dirty: utilizado na política de write-back, indica se é necessário fazer uma atualização no disco antes de sobrescrever a página na ram. se for 1 -> transfere a ultima versão da página na secundária, pra depois sobrescrever na RAM; se for 0 -> não há necessidade de atualização.

bit ref: utilizado nas políticas de substituição, se for 1 é referenciado; se for 0 não é




###### TLB


#### Swap

Descrição do processo de troca de páginas:

Uma página precisa ser transferida para a RAM, mas ela ta cheia - começa o swap. Se houve alguma alteração nessa página correspondente na RAM desde o momento que ela veio da secundária, o bit dirty é ligado. Se o bit dirty é 1, então o dado atualizado é transferido para a secundária pra, finalmente, ser sobreescrito. Se o bit dirty é 0, então não há necessidade de salvar aquela página na secundária antes de sobrescrevê-la, pois é a mesma.


#### Esquema final

![[Pasted image 20231126110416.png]]



![[Pasted image 20231126110833.png]]