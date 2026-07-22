---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware
criada: '2024-10-14'
---

## SRAM Technology

As SRAMs (Static Random-Access Memories) são circuitos integrados simples que consistem em matrizes de memória com geralmente apenas uma porta de acesso, que pode ser usada para leitura ou escrita. SRAMs têm um tempo fixo de acesso a qualquer dado, embora os tempos de acesso para leitura e escrita possam ser diferentes. Uma vantagem das SRAMs é que elas não precisam de atualização periódica (refresh), e, portanto, o tempo de acesso é muito próximo ao tempo do ciclo. O ciclo de tempo é o intervalo entre acessos à memória. Para garantir a integridade dos dados, as SRAMs normalmente usam de seis a oito transistores por bit. No passado, a maioria dos PCs e sistemas de servidores usava chips de SRAM separados para seus caches primários, secundários ou mesmo terciários. Atualmente, devido à Lei de Moore, todos os níveis de cache são integrados no próprio chip do processador, o que levou ao desaparecimento quase completo do mercado de chips de SRAM separados. Isso significa que os processadores modernos incorporam todos os níveis de cache, tornando os chips de SRAM independentes praticamente obsoletos.

### Síntese
	- As SRAMs são circuitos integrados simples que contêm matrizes de memória com uma única porta de acesso, permitindo leitura ou escrita.
	- As SRAMs possuem um tempo de acesso fixo, embora os tempos de leitura e escrita possam variar.
	- Elas não necessitam de atualização periódica (refresh) e têm tempos de acesso próximos ao ciclo de memória.
	- As SRAMs usam normalmente seis a oito transistores por bit para garantir a integridade dos dados.
	- No passado, os PCs e servidores usavam chips de SRAM separados para diferentes níveis de cache.
	- Atualmente, devido ao avanço da tecnologia (Lei de Moore), todos os níveis de cache são integrados nos chips de processadores, reduzindo a necessidade de chips de SRAM independentes.

## DRAM Technology

Em uma SRAM (Static Random-Access Memory), desde que haja energia aplicada, o valor pode ser mantido indefinidamente.

Em uma DRAM (Dynamic Random-Access Memory), o valor armazenado em uma célula é mantido como uma carga em um capacitor. Um único transistor é usado para acessar essa carga armazenada, seja para ler o valor ou para sobrescrever a carga armazenada. Por usar apenas um transistor por bit de armazenamento, as DRAMs são muito mais densas e econômicas por bit do que as SRAMs. No entanto, as DRAMs não podem manter a carga indefinidamente e devem ser periodicamente atualizadas. Essa falta de persistência é por isso que essa estrutura de memória é chamada de "dinâmica", em oposição ao armazenamento estático em uma célula SRAM.

Para atualizar a célula, basta ler seu conteúdo e escrevê-lo de volta. A carga pode ser mantida por vários milissegundos. Se cada bit tivesse que ser lido e escrito individualmente na DRAM, estaríamos constantemente atualizando a DRAM, o que deixaria pouco tempo para acessá-la. Felizmente, as DRAMs usam uma estrutura de decodificação de dois níveis, o que nos permite atualizar uma linha inteira (que compartilha uma linha de palavras) com um ciclo de leitura seguido imediatamente por um ciclo de escrita.

A organização de linhas que auxilia na atualização também beneficia o desempenho das DRAMs. Para melhorar o desempenho, as DRAMs armazenam linhas em um buffer para acesso repetido. Esse buffer funciona como uma SRAM; ao alterar o endereço, é possível acessar bits aleatórios no buffer até o próximo acesso à linha. Essa capacidade melhora significativamente o tempo de acesso, uma vez que o acesso aos bits na linha é muito mais rápido. Aumentar a largura do chip também melhora a largura de banda da memória do chip. Quando a linha está no buffer, ela pode ser transferida por meio de endereços sucessivos, na largura da DRAM (tipicamente 4, 8 ou 16 bits), ou especificando uma transferência de bloco e o endereço inicial no buffer.

Para melhorar ainda mais a interface com os processadores, as DRAMs adicionaram clocks e são corretamente chamadas de Synchronous DRAMs ou SDRAMs. A vantagem das SDRAMs é que o uso de um clock elimina o tempo necessário para a sincronização entre a memória e o processador. A vantagem de velocidade das SDRAMs síncronas vem da capacidade de transferir os bits em uma rajada (burst) sem a necessidade de especificar bits de endereço adicionais. Isso é chamado de Double Data Rate (DDR) SDRAM. O nome significa que as transferências de dados ocorrem nas bordas de subida e descida do clock, obtendo assim o dobro da largura de banda esperada com base na taxa de clock e largura de dados. A versão mais recente dessa tecnologia é chamada DDR4. Uma DRAM DDR4-3200 pode fazer 3200 milhões de transferências por segundo, o que significa que ela tem um clock de 1600 MHz.

Para sustentar tanta largura de banda, é necessária uma organização inteligente dentro da DRAM. Em vez de apenas um buffer de linha mais rápido, a DRAM pode ser organizada internamente para ler ou escrever em múltiplos bancos, cada um com seu próprio buffer de linha. O envio de um endereço para vários bancos permite que todos eles leiam ou escrevam simultaneamente. Por exemplo, com quatro bancos, há apenas um tempo de acesso e, em seguida, os acessos alternam entre os quatro bancos para fornecer quatro vezes a largura de banda. Esse esquema de acesso rotativo é chamado de interleaving de endereços.

Embora dispositivos pessoais móveis, como o iPad, usem DRAMs individuais, a memória para servidores é comumente vendida em pequenas placas chamadas módulos de memória de dupla linha (DIMMs). Os DIMMs normalmente contêm de 4 a 16 DRAMs e são normalmente organizados com uma largura de 8 bytes para sistemas de servidores. Um DIMM usando SDRAMs DDR4-3200 poderia transferir a uma taxa de 8 × 3200 = 25.600 megabytes por segundo. Esses DIMMs são nomeados de acordo com sua largura de banda, como PC25600. Como um DIMM pode ter muitos chips de DRAM, dos quais apenas uma parte é usada para uma transferência específica, precisamos de um termo para se referir ao subconjunto de chips em um DIMM que compartilha linhas de endereço comuns.

Para evitar confusão com os nomes internos de linha e bancos de DRAM, usamos o termo "rank de memória" para se referir a esse subconjunto de chips em um DIMM.

### Síntese:
	- Armazena dados como carga em capacitores.
	- Armazena dados em células adimensionais, endereçadas em bytes
	- Usa um único transistor por bit de armazenamento, o que a torna mais densa e econômica que a SRAM.
	- Requer atualização periódica devido à falta de persistência da carga.
	- A atualização da DRAM envolve ler o conteúdo e escrevê-lo de volta.
	- Organização de linhas ajuda na atualização e no desempenho.
	- Buffer de linhas ajuda a melhorar o acesso ao permitir o acesso a bits aleatórios no buffer.
	- Largura do chip afeta a largura de banda da memória.
	- SDRAMs usam clocks para melhorar a sincronização com processadores.
	- A tecnologia DDR (Double Data Rate) melhora a largura de banda com transferências nas bordas de subida e descida do clock.
	- DIMMs (Dual Inline Memory Modules) são usados em servidores, contendo vários chips de DRAM.
	- Termo "rank de memória" é usado para se referir a um subconjunto de chips em um DIMM que compartilham linhas de endereço comuns.


## Flash Memory

Flash memory is a type of electrically erasable programmable read-only memory (EEPROM). Unlike disks and DRAM, but like other EEPROM technologies, writes can wear out flash memory bits. To cope with such limits, most flash
products include a controller to spread the writes by remapping blocks that have been written many times to less trodden blocks. This technique is called wear leveling. With wear leveling, personal mobile devices are very
unlikely to exceed the write limits in the flash. Such wear leveling lowers the potential performance of flash, but it is needed unless higher-level software monitors block wear. Flash controllers that perform wear leveling
can also improve yield by mapping out memory cells that were manufactured incorrectly.
### Síntese:

	- Flash memory é um tipo de memória somente leitura programável eletricamente (EEPROM).
	- Diferentemente de discos rígidos e DRAM, mas semelhante a outras tecnologias EEPROM, a gravação pode desgastar os bits da flash memory.
	- Para lidar com esse desgaste, a maioria dos produtos de flash inclui um controlador que distribui as gravações, remapeando blocos que foram gravados muitas vezes para blocos menos utilizados. Esse processo é chamado de "wear leveling".
	- O wear leveling evita que dispositivos móveis pessoais excedam os limites de gravação na flash, embora possa reduzir o desempenho.
	- Controladores de flash que realizam wear leveling também podem melhorar o rendimento, mapeando as células de memória que foram fabricadas incorretamente.



## Disk Memory

As Figure 5.6 shows, a magnetic hard disk consists of a collection of platters, which rotate on a spindle at 5400 to 15,000 revolutions per minute. The metal platters are covered with magnetic recording material on both sides, similar to the material found on a cassette or videotape. To read and write information on a hard disk, a movable arm containing a small electromagnetic coil called a read-write head is located just above each surface. The entire drive is permanently sealed to control the environment inside the drive, which, in turn, allows the disk heads to be much closer to
the drive surface.

### Síntese:

	- Um disco rígido magnético é composto por um conjunto de pratos metálicos que giram em um eixo a velocidades entre 5400 e 15.000 rotações por minuto.
	- Esses pratos metálicos são revestidos com material de gravação magnética em ambos os lados, semelhante ao material encontrado em fitas cassete ou videoteipes.
	- Para ler e gravar informações em um disco rígido, um braço móvel contendo uma pequena bobina eletromagnética chamada cabeça de leitura e gravação está localizado logo acima de cada superfície do disco.
	- O disco rígido é hermeticamente selado para controlar o ambiente interno, permitindo que as cabeças de leitura e gravação fiquem muito próximas à superfície do disco.

