---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware/assembly
criada: '2024-10-14'
---

**Montagem (Assembly):**

- **O que faz:** Traduz o código assembly para linguagem de máquina.
- **Arquivo de entrada:** Arquivo fonte em linguagem assembly (geralmente com extensão `.s` ou `.asm`).
- **Arquivo de saída:** Arquivo objeto (geralmente com extensão `.o` ou `.obj`), que contém o código de máquina.
- **Comando típico:** `as` (Assembler).

**Linkagem:**

- **O que faz:** Combina arquivos objeto e bibliotecas para criar um executável.
- **Arquivo de entrada:** Arquivos objetos (resultantes da montagem) e bibliotecas.
- **Arquivo de saída:** Executável final.
- **Comando típico:** `ld` (Linker), embora seja comum usar um compilador que lida tanto com a montagem quanto com a linkagem (como `gcc`).


Então, em um fluxo típico:

1. **Montagem:**
    
    - Você escreve o código em linguagem assembly.
    - Usa o assembler (`as`) para converter o código para linguagem de máquina.
    - Gera arquivos objeto (`.o`).
2. **Linkagem:**
    
    - Usa o linker (`ld` ou integrado em um compilador como `gcc`) para combinar arquivos objetos e bibliotecas.
    - Gera um executável final.

O compilador é frequentemente usado para lidar com ambas as etapas, simplificando o processo para o desenvolvedor. Quando você usa um comando como `gcc`, ele chama o assembler para cada arquivo de origem (C ou assembly), obtém arquivos objetos e, em seguida, chama o linker para gerar o executável final


## Pilha e Pilha de execução


#### Diferença entre heap e stack

Heap e stack são duas áreas de memória usadas para armazenar dados de maneiras diferentes em um programa.

1. **Heap:**
    - **Alocação:** A alocação de memória no heap é dinâmica, e o programador é responsável por solicitar e liberar memória explicitamente.
    - **Vida Útil:** A vida útil da memória alocada no heap não está vinculada a um escopo específico e pode persistir além do término de uma função.
    - **Uso Típico:** É comumente usado para armazenar dados que precisam ser acessados globalmente ou por várias partes do programa.
    - **Risco:** Exige gerenciamento manual e pode levar a vazamentos de memória se não for tratado corretamente.
2. **Stack:**
    - **Alocação:** A alocação de memória na stack é automática e gerenciada pelo compilador. Cada função tem seu próprio bloco de memória na stack.
    - **Vida Útil:** A memória alocada na stack está vinculada ao escopo de uma função e é liberada automaticamente quando a função retorna.
    - **Uso Típico:** É usado para armazenar variáveis locais, ponteiros e informações de contexto durante a execução de uma função.
    - **Eficiência:** Acesso rápido e eficiente, pois a alocação e desalocação são apenas movimentações do ponteiro da stack.

Em resumo, a principal diferença entre heap e stack está na forma como a memória é alocada e desalocada, na vida útil dos dados e na responsabilidade do programador. O heap oferece flexibilidade, mas requer gerenciamento manual, enquanto a stack é mais eficiente e gerenciada automaticamente pelo sistema.


#### Memory segmentation

![[WhatsApp Image 2023-12-02 at 15.50.28.jpeg]]