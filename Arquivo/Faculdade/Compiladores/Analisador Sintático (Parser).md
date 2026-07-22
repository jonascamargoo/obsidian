---
tipo: conceito
area: Compiladores
tags:
- compiladores
criada: '2025-04-10'
---

## O que é?

Segunda etapa de compilação. O **analisador sintático** (ou *parser*) opera sobre a **saída** do Analisador Léxico. Sua principal entrada é a **Fila de Tokens**, uma sequência linear das unidades léxicas identificadas no código-fonte. A função do parser é verificar se essa sequência de tokens **obedece às regras gramaticais** da linguagem de programação. Ele faz isso tentando construir uma **árvore sintática (ou árvore de derivação / AST - Abstract Syntax Tree)**. 

Essa árvore representa a estrutura hierárquica do código: cada nó ou subárvore corresponde a uma construção da linguagem, como uma declaração, uma expressão, um comando de controle (if, while), etc. Se a sequência de tokens puder ser organizada em uma árvore válida de acordo com a gramática, o código está sintaticamente correto. Caso contrário, se um token não se encaixar na estrutura esperada pela gramática, o parser reporta um **erro de sintaxe**.

A **raiz da árvore sintática** costuma representar o ponto de entrada do programa, como `Programa` ou `Main`, dependendo da gramática. Cada comando ou expressão vira uma subárvore ligada à raiz.

Exemplo:

```c
int x = 5;

```


Gera tokens como: `int` `x` `=` `5` `;`, e o parser constrói uma subárvore representando uma declaração de variável com atribuição.

O parser consulta as **regras da gramática**, geralmente organizadas em uma **lista ordenada de produções**, para verificar se a sequência de tokens pode ser derivada a partir do símbolo inicial da linguagem. Se algum token não puder ser encaixado em nenhuma regra válida, ocorre um erro de **sintaxe**.

> 🔄 Em linguagens com suporte a **paralelismo ou concorrência**, o compilador pode adaptar a forma como interpreta e constrói essas subárvores para melhor paralelizar a execução ou a análise posterior.

## 🌳 Árvore de Instruções vs Árvore de Frases

Durante a **análise sintática**, o compilador constrói uma **árvore sintática** (também chamada de _parse tree_ ou _syntax tree_) com base na **gramática da linguagem**. Essa árvore representa a **estrutura hierárquica** do código-fonte. Essa árvore geralmente pode ser pensada em **duas grandes camadas ou divisões**:

### 🌲 **Árvore de Instruções** (Instruction Tree)

A árvore de instruções representa **o corpo principal do programa**, com **cada instrução como um nó ou subárvore**. Aqui, o foco está na **sequência de ações** que o código realiza. Por exemplo, considere o seguinte trecho:

```c
x = a + b;
y = x * 2;
```

A árvore de instruções ficaria assim:

```c
Programa
├── Atribuição: x = a + b
└── Atribuição: y = x * 2
```

Cada linha de código (ou bloco, como um `if`, `while`, `for`) é **uma subárvore** da árvore principal.

> 🧠 Essa árvore ajuda a **identificar a estrutura lógica** do programa — o que será executado e em que ordem.


### 🌿 **Árvore de Frases** (Phrase Tree)

Dentro de cada instrução, temos **frases gramaticais** da linguagem — como expressões aritméticas, chamadas de função, condições, etc. A árvore de frases representa **a estrutura interna de cada instrução**, ou seja, **como os elementos daquela linha se relacionam**.

Voltando ao exemplo anterior:

```c
x = a + b;

```

A árvore de frases para essa linha seria:

```c
Atribuição
├── Identificador: x
└── Expressão
    ├── Identificador: a
    ├── Operador: +
    └── Identificador: b
```

Essa parte da árvore mostra **a gramática interna da linguagem**, revelando a **precedência dos operadores**, **a forma das expressões**, **estrutura de chamadas de função**, etc.

🔎 É na árvore de frases que o compilador verifica coisas como:

- Ordem de avaliação
    
- Tipos de dados envolvidos
    
- Coerência gramatical da linguagem

### Analogia com Língua Portuguesa (pra fixar!)

Imagine a frase:

> "O cachorro latiu alto."

- A **árvore de instruções** seria como dizer: "Essa é uma sentença completa — uma ação."
    
- A **árvore de frases** divide isso em: sujeito ("O cachorro"), verbo ("latiu") e complemento ("alto").
    

---

### Por que essa divisão é útil?

Separar a árvore sintática nessas duas visões ajuda o compilador (e a gente!) a:

- Organizar melhor o código internamente.
    
- Otimizar instruções com mais eficiência.
    
- Facilitar a geração de código intermediário.
    
- Adaptar a compilação para execução paralela ou otimizada.
    
- Suportar melhor a análise semântica posterior.


### Gramática Formal, Ambiguidade e o Desafio da Linguagem Natural

O "dicionário" que o analisador sintático consulta é, na verdade, uma **gramática formal** que define todas as regras estruturais da linguagem. Essa gramática é comumente expressa em uma notação chamada **BNF (Backus-Naur Form)**. Quando a gramática é definida de forma estrita e sem ambiguidades, ferramentas conhecidas como *compiler-compilers* (ex: YACC, ANTLR) conseguem ler o arquivo BNF e gerar o código de um analisador sintático funcional automaticamente.

É na análise sintática que a diferença entre linguagens de programação e linguagens naturais se torna gritante:

* **Linguagens de Programação e Ambiguidade:** São projetadas para serem **livres de ambiguidade**. Uma expressão como `x = a + b;` deve ter apenas uma interpretação estrutural válida. O parser, portanto, gera uma única e determinística Árvore Sintática Abstrata (AST).

* **Linguagens Naturais e Ambiguidade:** A **ambiguidade é a regra**. Uma frase como "Eu vi o homem na montanha com o telescópio" pode gerar múltiplas árvores sintáticas válidas. O desafio do parser de uma LN é ser capaz de reconhecer todas as estruturas possíveis e, em fases posteriores (semântica), tentar determinar a mais provável. Por isso, como regra geral, **quanto mais aberta e flexível for a linguagem, mais complexidade é transferida do analisador léxico para o sintático e semântico**.

* **Paralelismo:** Em linguagens que suportam concorrência, a forma como as subárvores são construídas pode ser adaptada para facilitar a análise e a execução paralela das instruções.


