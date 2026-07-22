# Sistemas Operacionais - Memória Virtual

## Retirados do livro -> Sistemas Operacionais Modernos (Andrew S. Tanenbaum, Herbert Bos) 4ª

## 4 - Estratégias de Alocação de Memória

Considere um sistema de troca no qual a memória consiste nos seguintes tamanhos de lacunas na ordem da memória: 10 MB, 4 MB, 20 MB, 18 MB, 7 MB, 9 MB, 12 MB e 15 MB. Qual lacuna é pega para sucessivas solicitações de segmentos de:

(a) 12 MB  
(b) 10 MB  
(c) 9 MB  

| Estratégia | Primeira lacuna alocada | Segunda lacuna alocada | Terceira lacuna alocada |
|------------|-----------------------|------------------------|------------------------|
| First Fit  | 20 MB                 | 10 MB                  | 18 MB                  |
| Best Fit   | 12 MB                 | 10 MB                  | 9 MB                   |
| Worst Fit  | 20 MB                 | 18 MB                  | 15 MB                  |
| Next Fit   | 20 MB                 | 18 MB                  | 9 MB                   |

---

## 5 - Diferença entre Endereço Físico e Virtual

- **Endereço físico:** Composto pela memória RAM, onde os dados estão de fato armazenados. O espaço de endereçamento corresponde ao espaço da memória RAM e é limitado pela arquitetura.
- **Endereço virtual:** Limitado pela arquitetura, traduzido para o endereço físico através da page table.

---

## 7 - Conversão de Endereço Virtual para Físico

Usando a tabela de páginas da Figura 3.9:

- (a) 20 → 8.212  
- (b) 4.100 → 4.100  
- (c) 8.300 → 24.684  

O endereço físico é obtido somando a base da página ao offset (endereço virtual módulo tamanho da página).

---

## 9 - Suporte de Hardware para Memória Virtual

- **Page Table Register (PTR):** Armazena o endereço base da page table na memória.
- **TLB (Translation Lookaside Buffer):** Cache para acelerar a tradução de endereços.
- **Mecanismo de tratamento de exceções:** Detecta page faults e redireciona para o kernel.
- **MMU (Memory Management Unit):** Traduz endereços virtuais para físicos e interage com TLB e page table.

---

## 16 - Tempo de Tradução de Endereço

Dado:

- **TLB:** 1024 entradas, acesso em 1 ciclo (1 ns)
- **Tabela de páginas:** Acesso em 100 ciclos (100 ns)
- **Substituição de página:** 6 ms
- **Taxa de acerto na TLB:** 99%
- **Taxa de falha na TLB:** 1%
- **Taxa de page fault:** 0,01%

Fórmula:

\[ EAT = (0.99 \times 1) + (0.01 \times 100) + (0.0001 \times 6.000.000) \]

Resultado: **602 ciclos de clock**

---

## 27 - Problema de Algoritmos de Substituição de Página

Sequência: 0, 1, ..., 511, 431, 0, 1, ..., 511, 332, 0, 1, ...

- LRU, FIFO e Relógio não são eficazes quando a alocação de páginas é menor que 512.
- Causam page faults contínuos.
- Melhor abordagem: reservar 498 quadros para a sequência fixa e usar 2 quadros para páginas aleatórias.

---

## 28 - Cálculo de Page Faults

Sequência: **0172327103** com **4 quadros**

| Algoritmo | Page Faults |
|-----------|------------|
| FIFO      | 6          |
| LRU       | 7          |

---

## 31 - Diferença entre LRU e Algoritmo de Relógio

Sequência: **0, 1, 2, 1, 2, 0, 3** com **3 quadros**

- **LRU:** Remove a página menos usada recentemente (Página 1).
- **Relógio:** Usa um ponteiro circular e substitui a página 1 por 3.

---

# Memória Virtual

## Conceito e Funcionamento

- Cada processo possui um espaço de endereçamento virtual.
- Esse espaço é mapeado para a memória física, permitindo mais eficiência e segurança.
- Page table armazena esse mapeamento.
- Em caso de **page fault**, os dados são buscados no disco.

## Tradução Rápida - TLB

- Pequeno cache de traduções recentes entre endereços virtuais e físicos.
- Se houver um **TLB miss**, a tradução ocorre via page table.

## Diferença entre CPU e MMU

| Componente | Função |
|------------|--------|
| **CPU** | Gera o endereço virtual e acessa o TLB. |
| **MMU** | Tradução do endereço virtual para físico, interage com TLB e page table. |

## Offset na Memória Virtual

- O **offset** indica a posição dentro da página.
- Um endereço virtual é dividido em:
  - **Número da Página Virtual (VPN)**
  - **Offset** (posição dentro da página)
