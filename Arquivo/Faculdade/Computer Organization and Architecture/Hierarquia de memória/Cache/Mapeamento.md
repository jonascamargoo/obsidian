---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware
criada: '2024-10-14'
---

### Mapeamento direto

A memória é endereçada por bytes, ou seja, cada célula de memória carrega um byte. A maneira mais simples de atribuir um local na cache para cada palavra na memória é basear-se no endereço da palavra na memória. Essa estrutura de cache é chamada de "mapeamento direto", pois cada local de memória é mapeado diretamente para exatamente um local na cache. A correspondência típica entre endereços e locais de cache para uma cache de mapeamento direto é geralmente simples e direta. Nesse tipo de cache, o endereço de uma palavra na memória é usado para determinar sua posição correspondente na cache. Quando é necessário acessar essa palavra novamente, a cache pode ser consultada diretamente usando o mesmo cálculo do endereço. Portanto, encontrar um item na cache é eficiente, mas o mapeamento direto pode ser limitante, uma vez que cada local de memória só pode ser armazenado em uma localização específica da cache. Isso pode levar a problemas de desempenho quando há muitos acessos simultâneos a diferentes localizações da memória que mapeiam para o mesmo local na cache.

"Direct-mapped cache" -> *A cache structure in which each memory location is mapped to exactly one
location in the cache.*

![[Pasted image 20231025204036.png]]


Primeira forma -> Endereçamento direto (Direct-mapped cache): *i* =  *(Endereço de bloco) mod (Número de blocos de cache na cache)*, Sendo *i* o número da linha da cache. Se o número de entradas na cache for uma potência de dois, então, o módulo pode ser calculado simplesmente usando os log 2 bits menos significativos sobre o tamanho da cache em blocos.
#### Tag

A cache armazena dados da memória principal em seus locais específicos. Como um único local na cache pode conter dados de diferentes locais na memória, é necessário um meio de identificar se os dados armazenados na cache correspondem à palavra de memória requisitada. Para isso, são usadas tags, que são informações de endereço adicionadas a cada entrada da cache. As tags identificam se a word na cache corresponde à word requisitada. Elas contém informações de endereço para identificar se a word na cache corresponde à word requisitada. As tags normalmente contêm a parte superior do endereço, que não é usada como índice para a cache, permitindo a comparação com o endereço da palavra requisitada.

#### Bit de validade

Quando um processador é iniciado, a cache não contém dados válidos, e os campos de tag podem não ter significado. Mesmo após a execução de muitas instruções, alguns locais na cache podem estar vazios, o que significa que não contêm dados válidos.  Para identificar esses casos, um "bit de validade" é utilizado. Se o bit de validade não estiver ligado (ou seja, for igual a zero), isso indica que não há correspondência entre a entrada da cache e a palavra requisitada.  Esse bit de validade ajuda a garantir que apenas dados válidos e relevantes sejam utilizados na cache
#### O processo de comparação

O processador possui o endereço da palavra de memória que deseja acessar -> Antes de verificar a cache, o processador extrai a parte superior do endereço, que é a "tag" -> A tag é usada para identificar a palavra específica na memória principal que está sendo acessada -> O processador compara a tag da palavra de memória com as tags armazenadas em todas as entradas da cache -> Cada entrada da cache possui uma tag que corresponde à palavra de memória armazenada naquele local da cache ->  Ao comparar as tags, o processador também verifica o "bit de validade" associado a cada entrada da cache -> Se o bit de validade estiver ligado, isso indica que os dados naquela entrada da cache são válidos e relevantes.

Dito isso, há três possíveis resultados após a comparação das tags e bits de validade:

1 -  Se uma correspondência é encontrada (a tag na cache coincide com a tag da palavra de memória e o bit de validade está ligado), isso é chamado de "acerto na cache" (cache hit), e os dados são lidos diretamente da cache, economizando tempo, sem precisar buscar na principal, ou seja, sem mapeamento;

2-  Se não houver correspondência entre as tags (ou seja, a tag na cache não coincide com a tag da palavra de memória) ou o bit de validade estiver desligado, isso é chamado de "erro na cache" (cache miss), e os dados precisam ser buscados na memória principal e, em seguida, carregados na cache para acessos posteriores;

3 - Se a cache estiver vazia (sem entradas com tags válidas), será necessária uma busca na memória principal, uma vez que não há dados na cache.

OBS: Quando há cache hit, a CPU continua. Quando há chace miss, o pipeline é parado e busca-se o próximo nível da hierarquia *L(n+1)* .

#### Subdivisão do endereço

![[Pasted image 20231025215837.png]]

Sobre o Byte offset -> serve para identificar qual realmente será o byte ou word a ser acessado dentro da cache (pois geralmente cada bloco tem mais de uma word - princípio da localidade espacial)



##### Exemplo: Considere 64 blocos, 16 bytes por bloco. Para qual linha o endereço 1200 é mapeado?

resolução: 1200/16 = 75. Como 75 % 64 = 11. Então *i* = 11, e ficaria assim:

![[Pasted image 20231025221357.png]]

byte offset = 4, pois temos dentro do bloco 16 bytes e precisamos de 4 bits para comportar as 16 escolhas;
index = 6 bits, pois temos 64 blocos armazenados na cache, que podem ser comportados em apenas 6 bits;


#### Tamanho de uma cache

* O Número de bits necessários para uma cache é uma função do tamanho da cache e do tamanho do endereço, pois a cache inclui o armazenamento para os dados e as tags;

* Para explorar de maneira eficiente o princípio da localidade espacial, o tamanho do bloco deve ser de várias words. OBS: blocos maiores reduzem miss, pelo princípio da localidade, porém se a cache não aumentar também, pois ai haveria muitas colisões, consequentemente, muito miss;

-  Geralmente, o valor de uma cache é apresentado considerando apenas a quantidade de memória disponível para dados, não da cache inteiro (apenas valores uteis de memória que poderiam ser utilizados).

* Considerando o endereço em bytes de 32 bits, uma cache diretamente mapeada de 2^n blocos de tamanho com 2^m words (2^(m+2) bytes) por bloco
	* Ela exigirá um campo tag cujo tamanho é 32 – (n+m+2) bits, pois n bits são usados para o índice, m bits são usados para a word dentro do bloco e 2 bits são usados para a parte do byte do endereço
	* O número total de bits de uma cache diretamente mapeada é:
		* (2^n) * (tamanho do bloco + tamanho da tag + tamanho do campo de validade)
	- Como o tamanho do bloco é 2^m words (2 m+5 bits) e o tamanho do endereço é 32 bits, o número de bits nessa cache é : (2^n) * (2^m * 32 +(32 – n – m - 2)+ 1) = (2^n) * ((2^m) * 32 + 31 – n - m).

##### Exemplo: Quantos bits no total são necessários para uma cache com mapeamento direto com 128 KB de dados e tamanho de bloco com 1 word, considerando um endereço de 32 bits?

resolução: 

128 KB = (2^7)*(2^10) = 2^17 bytes. Como 1 word possui 4 bytes, então são (2^17)/4 = 2^15 words. Como só tem uma word por bloco, 2^15 blocos. 

tamanho da entrada da cache = bits bloco de dados + bits tag +  bits validade. Tem-se 1 bit de validade; para o bloco de dados temos 32;  Para o campo tag, sabemos que 15 bits serão utilizados para o índice, e 2 para o offset dentro da word. Logo, 32 + (32 - 15 - 2) + 1 = 48 bits. Portanto, o tamanho da cache é 2¹⁵ * 48 = 1.5 Mbits.

Como ficaria o mesmo exemplo, porém com 4 words por bloco? 2¹⁵ / 4 = 2¹³ blocos, então 13 bits para índices e  4 para o campo de word. Como são 32 bits para cada word e temos 4 por linha, então os bits do bloco de dados são 128. Temos 4 bits para o offset (conseguimos comportar as  16 possíveis escolhas de bytes em 4 bits). Fica: 128 - (32 - 13 - 4) + 1 = 144 bits, vezes a quantidade de linhas (2¹³), temos que o número de bits nesse cache é 1.25 Mbits. 

##### Exemplo: Faça uma tabela que represente o estado de uma cache com 8 blocos de 1 word em uma arquitetura de 64 bits, após a seguinte sequência de endereços de bytes acessados pela CPU. Para cada acesso, informe se houve hit ou miss na cache. Refaça a mesma questão considerando que a sequência de endereços agora representam endereços de word. Endereços: 0, 64, 4, 68, 64, 1. Por fim, diga quantos bits são necessários para implementar essa memória cache.

Resolução:

Estado inicial. Arq de 64 bits com 1 word (64 bits ou 8 bytes)por bloco, então offset de 3 bits (para comportar 8 possíveis valores para a memória) e 2 de índice (para comportar 4 linhas)

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|0|-|-|
|01|0|-|-|
|10|0|-|-|
|11|0|-|-|

0 -> 0000…0000 0000 miss. 

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|**[0]** [1] [2] [3] [4] [5] [6] [7]|
|01|0|||
|10|0|||
|11|0|||

1 -> 0000…0000 0001 hit, pois acabou de ser escrito. Os 3 lsd são de offset (001) e os 2 em seguida são index (00). A word no bloco nãos erá alterada, pois é a mesma word que carrega o endereço 0 (lembrando que pegamos a word inteira, então buscamos o endereço 2 ou 3 ou 4, da no mesmo, pois estão na mesma word então teremos que trazer ela da memória, para então o offset pegar o que queremos).

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|[0] **[1]** [2] [3] [4] [5] [6] [7]|
|01|0|||
|10|0|||
|11|0|||


7 -> 0000....0000 0111 hit

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|[0] [1] [2] [3] [4] [5] [6] **[7]**|
|01|0|||
|10|0|||
|11|0|||

8 -> 0000...0000 1000 miss

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|[0] [1] [2] [3] [4] [5] [6] [7]|
|01|1|0…000 (59 bits)|**[8]** [9] [10] [11] [12] [13] [14] [15]|
|10|0|||
|11|0|||

10 -> 0000...0000 1010 hit

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|[0] [1] [2] [3] [4] [5] [6] [7]|
|01|1|0…000 (59 bits)|[8] [9] **[10]** [11] [12] [13] [14] [15]|
|10|0|||
|11|0|||

17 -> 0000...001 0001

|   |   |   |   |
|---|---|---|---|
|Index|V|Tag|Data (8 bytes)|
|00|1|0…000 (59 bits)|[0] [1] [2] [3] [4] [5] [6] [7]|
|01|1|0…000 (59 bits)|**[8]** [9] [10] [11] [12] [13] [14] [15]|
|10|1|0…000 (59 bits)|[17] [18] [19] [20] [21] [22] [23]|
|11|0|||

Refazendo para bytes


Calculando a quantidade de bits necessários para implementar a cache -> 4 * 124


#### Faça o mesmo exercício, porém com arquitetura de 16 bits, 8 blocos e endereços: 2, 3, 0, 1, 16, 1.

Estado inicial. Há 8 blocos, então 3 bits para índice. Cada word nessa arquitetura tem 2 bytes e há uma word por linha, então cada linha tem 2 bytes  

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (10 bits)|Data (2 bytes)|
|000|0|||
|001|0|||
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||


2 -> 0000 0000 0000 0010 miss
  
|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|0|||
|001|1|0…0000 0000|**[2]** [3]|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||

3 -> 0000 0000 0000 0011 hit

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|0|||
|001|1|0…0000 0000|[2] **[3]**|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||

0 -> 0000 0000 0000 0000 miss

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|1|0…0000 0000|**[0]** [1]|
|001|1|0…0000 0000|[2] [3]|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||

1 -> 0000 0000 0000 0001 hit

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|1|0…0000 0000|[0] **[1]**|
|001|1|0…0000 0000|[2] [3]|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||

16 -> 0000 0000 0001 0000 miss (tag diferente)

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|1|0…1000 0000|**[16]** [17]|
|001|1|0…0000 0000|[2] [3]|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||


1 -> 0000 0000 0000 0001 miss (foi sobrescrita na última operação)

|   |   |   |   |
|---|---|---|---|
|Index (3 bits)|V (1 bit)|Tag (12 bits)|Data (2 bytes)|
|000|1|0…0000 0000|[00] **[01]**|
|001|1|0…0000 0000|[2] [3]|
|010|0|||
|011|0|||
|100|0|||
|101|0|||
|111|0|||

Refazendo com endereçamento em words (FAZER DEPOIS, só multiplicar o endereço por 4)


Agora, calculando a quantidade x de bits necessários para implementar essa cache: tamanho vezes largura da tabela. Sei que a arquitetura é de 16 bits, então cada endereço que chega tem 16 bits, sendo 1 de verificação, 1 de offset (para comportar qual dos 2 bytes serão escolhidos na word) e o resto é da tag. Além disso, na nossa linha também teremos os bits de dados, nesse caso, 16. Portanto

x = 8 * largura
x = 8 * ( 16 + (16 - 3 - 1) + 1) = 232 bits



### Mapping an Address to a Multiword Cache Block

Consider a cache with 64 blocks and a block size of 16 bytes. To what block number does byte address 1200 map? R: (Block address) modulo (Number of blocks in the cache), where the address of the block is:

$$\frac{byteAddress}{bytes \, per \, block}$$

Notice that this block address is the block containing all addresses between:
$$\frac{byteAddress}{bytes \, per \, block} \,X \,bytes \, per \, block$$

And:
$$\frac{byteAddress}{bytes \, per \, block} \,X \,bytes \, per \, block \, + \, (bytes \, per \, block\,-1)$$

Thus, with 16 bytes per block, byte address 1200 is block address
$$\frac{1200}{16}\,=\,75$$
which maps to cache block number (75 modulo 64) = 11, so, the 1200 byte is in 11 block of 16. In fact, this block maps all addresses between 1200 and 1215.