## Retirados do livro -> Sistemas Operacionais Modernos (Andrew S. Tanenbaum, Herbert Bos) 4ª

### 11. A alocação contígua de arquivos leva à fragmentação de disco

A fragmentação mencionada no texto refere-se à fragmentação interna, pois o espaço desperdiçado está dentro do bloco. Isso acontece de forma semelhante na memória virtual quando utilizamos segmentação. Cada processo precisa de um espaço contíguo para cada segmento, e se houver pequenos buracos na memória, um segmento maior pode não caber, mesmo que o espaço livre total seja suficiente.

### 12. Efeitos de um bloco de dados corrompido

(a) **Contíguo:** Se um bloco for corrompido, uma parte específica do arquivo será danificada. Como os blocos são contíguos, a corrupção afeta apenas aquela parte específica dos dados, sendo possível acessar o restante do arquivo (porém a leitura será incompleta).

(b) **Encadeado:** Cada bloco contém um ponteiro para o próximo bloco. Se o bloco for corrompido, perdemos o ponteiro para o próximo bloco, podendo gerar a perda geral do arquivo, pois não conseguimos saber o caminho restante.

(c) **Indexado (ou baseado em tabela):** Existe uma estrutura (índice) que armazena os endereços dos blocos do arquivo. Se um bloco de dados for corrompido, apenas aquele bloco é afetado. Como a posição dos outros blocos é conhecida, o resto do arquivo permanece acessível.

### 13. Cálculo do tempo de compactação do disco

Para leitura: 8KB/80MB = 0,1ms Tempo total para leitura: 5 + 4 + 0,1 = 9,1 ms Tempo total para ler e escrever: 9,1 + 9,1 = 18,2 ms Metade do disco: 8GB = 1.048.576 blocos Tempo total para mover todos os arquivos: 1048576 * 18,2 ms = 5,3 horas

### 14. Faz sentido compactar o disco?

Não faz sentido. A compactação levaria cerca de 5 horas para metade do disco, o que é impraticável para sistemas reais. Além disso, o sistema ficaria inutilizável durante a compactação e haveria um desgaste excessivo do disco.

### 16. Tamanho do maior arquivo possível

Considerando blocos de 1 KB e 10 endereços diretos de 8 bytes cada, temos: 1 KB = 1024 Bytes → 1024/8 = 128 endereços apontados pelo bloco indireto. Total: 138 blocos * 1 KB = **138 KB**.

### 17. Melhor esquema de alocação para históricos de estudantes

O esquema **indexado por tabela** é o mais apropriado porque:

- Permite acesso aleatório direto a qualquer parte do arquivo.
    
- Funciona bem com registros de tamanho fixo.
    
- A alocação contígua dificultaria expansões.
    
- A alocação encadeada não é eficiente para acesso aleatório.
    

### 18. Melhor esquema de alocação para arquivos de tamanho variável (4 KB a 4 MB)

O esquema **indexado por tabela** também é o mais apropriado porque:

- Adapta-se bem a tamanhos variáveis.
    
- Permite acesso direto eficiente.
    
- A alocação contígua dificultaria expansões.
    
- A alocação encadeada não permite acesso rápido.
    

### 23. Endereços de blocos em um disco de 4 TB com blocos de 4 KB

4TB / 4KB = X Como cada bloco usa 4KB, então Y/4KB = resultado

### 26. Perda do mapa de bits ou lista de livres

**UNIX (mapa de bits):** Recuperável com uma varredura completa do sistema de arquivos.

**FAT-16 (lista encadeada):** Parcialmente recuperável, mas com maior risco de perda de dados.

---

## Reflexão sobre a trajetória profissional e o QuintoAndar

O que mais me atrai no QuintoAndar não é apenas o produto, mas a trajetória que levou ao seu sucesso. Acredito que a empresa tem muito a me ensinar, permitindo que eu contribua tanto para o produto quanto para meu próprio desenvolvimento profissional. Vejo essa oportunidade como uma chance valiosa de vivenciar a experiência de trabalhar em uma empresa responsável por um dos maiores cases de sucesso.

Durante a graduação, enfrentei desafios que nunca poderia imaginar. Algo que considerava “simples”, como trabalhar em equipe, revelou-se um dos mais difíceis de lidar. Diferente de qualquer algoritmo ou estrutura de dados, alinhar nosso trabalho com o de outras pessoas não é uma habilidade que se aprende de forma linear. O desafio pode variar, mas está sempre presente. Ter essa consciência foi essencial para reconhecer a importância da organização e entender como ela ajuda a solucionar esses problemas. Por fim, a maior lição que aprendi foi que, quando algo é feito da maneira correta, adapta-se com mais facilidade às mudanças.