---
tipo: conceito
area: Banco de dados
tags:
- dados/sql
criada: '2024-10-14'
---

## Definição
### Chaves Primárias (PK)

A **chave primária** consiste em uma ou mais colunas cujos dados contidos são usados para identificar exclusivamente cada linha na tabela. Você pode pensar neles como um endereço. Se as linhas de uma tabela fossem caixas de correio, a chave primária seria a listagem de endereços de rua. Algumas condições devem ser atendidas para essa classificação:

- As colunas que definem a chave primária são exclusivas
- Cada coluna pode conter valores duplicados; no entanto, a combinação de valores de coluna é exclusiva
- Nenhum valor nas colunas de chave primária é NULL. Eu também estenderia isso para incluir valores “em branco”
- Ao definir uma tabela, você especifica a chave primária. Uma tabela possui apenas uma chave primária e sua definição é obrigatória
- As chaves primárias são armazenadas em um índice
- O índice mantém o requisito de exclusividade da chave primária. Também torna mais fácil para os valores de chave estrangeira se referirem aos valores de chave primária correspondentes, como aprenderemos na seção a seguir.


### Chaves Estrangeiras (FK)

Uma **chave estrangeira** é um conjunto de uma ou mais colunas em uma tabela que se refere à chave primária em outra tabela. Não há nenhum código especial, configurações ou definições de tabela que você precise colocar para “designar” oficialmente uma chave estrangeira.

## Exemplo

No diagrama abaixo, observe a tabela **CABECALHO_PEDIDO_VENDA**. A coluna **CABECALHO_PEDIDO_VENDA**.**Codigo_Taxa_Cambio** é uma chave estrangeira, pois está relacionada ao **TAXA_CAMBIO**. **Codigo_Taxa_Cambio**. Esta coluna **TAXA_CAMBIO**. **Codigo_Taxa_Cambio** é a chave primária da tabela **TAXA_CAMBIO**.

![[Pasted image 20240115094607.png]]

## Restrições de Chave Estrangeira

Uma restrição de chave estrangeira impede que você insira valores que não são encontrados na chave primária da tabela relacionada: Usando o primeiro diagrama como nosso exemplo, você não pode inserir **CABECALHO_PEDIDO_VENDA.Codigo_Taxa_Cambio se ainda não existir na tabela TAXA_CAMBIO**.
#### Essas restrições entram em vigor de várias maneiras:

1. Eles impedem que você altere o valor da chave estrangeira para um que não exista como um valor na chave primária da tabela relacionada.
2. Eles impedem que você exclua uma linha da tabela de chave primária. Isso impede que você crie registros órfãos. Registros órfãos são descritos como “registros filhos sem pais”.
3. Eles impedem você de adicionar um valor de chave estrangeira que não existe na chave primária.



![[Pasted image 20240115095208.png]]

