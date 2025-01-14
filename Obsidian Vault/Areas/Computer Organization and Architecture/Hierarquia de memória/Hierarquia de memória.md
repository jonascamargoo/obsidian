Conhecimento baseado no livro *computer organization and design the hardware/software interface*

A structure that uses multiple levels of memories; as the distance from the processor increases, the size of the memories and the access time both increase.

![[Pasted image 20231019090907.png]]


A hierarquia pode ter vários levels, mas os dados são transferidos apenas entre dois. A transferência da dados do registrador para a cache é feita em words, mas em qualquer level abaixo é feita em *blocos*: block (or line) The minimum unit of information that can be either present or not present in a cache.
Todo conjunto de dados presente no dado acima é um subconjunto do conjunto de dados abaixo, isto é, o level mais abaixo contém todos os dados do sistema - "*data cannot be present in level i unless it is also present in level i + 1.*"

#### Hit and miss

Se o dado requisitado pelo processador estiver em um level superior de memória, chama-se hit e, caso contrário, miss. *Taxa de hit*: hit rate Th e fraction of memory accesses found in a level of the memory hierarchy. *Taxa de miss*:  miss rate The fraction of memory accesses not found in a level of the memory hierarchy, (1−hit rate).

O principal motivo de dispor a memória em hierarquias é performance Since performance is the major reason for having a memory hierarchy, the time to service hits and misses is important. O *Hit time* é o tempo necessário para acessar o nível superior da hierarquia de memória, o que inclui o tempo necessário para determinar se o acesso é um acerto ou uma falha (ou seja, o tempo necessário para verificar os livros na mesa). O miss penalty é o tempo requerido para fazer um fetch de um block em level menor, incluindo o tempo de acesso ao bloco, a transmissão de um level para o outro e a inserção do bloco no level requisitado e, por fim, passar o bloco para o requestor. O tempo de acerto será muito menor do que o tempo de acesso ao próximo nível na hierarquia, que é o componente principal do Penalty time. (O tempo para examinar os livros na mesa é muito menor do que o tempo para levantar e pegar um novo livro nas prateleiras.)



