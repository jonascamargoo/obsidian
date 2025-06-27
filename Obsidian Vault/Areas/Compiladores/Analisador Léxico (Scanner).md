
Primeira etapa de compilação. O **analisador léxico** é responsável por ler o código-fonte caractere por caractere e agrupar esses caracteres em **lexemas**, formando **tokens** válidos segundo a linguagem de programação. Cada token representa uma unidade sintática básica, como palavras-chave (`if`, `while`), identificadores (`x`, `nome`), operadores (`+`, `==`), delimitadores (`;`, `{`, `}`), entre outros.

💡 Um **token** é tudo aquilo que está contido entre **separadores**, como espaços em branco, quebras de linha e símbolos.

```c
int idade = 20;

```

Os tokens seriam:

- `int` → palavra-chave
    
- `idade` → identificador
    
- `=` → operador
    
- `20` → literal inteiro
    
- `;` → delimitador

Por exemplo, a palavra `čachorro` contém um caractere inválido (`č`) que não faz parte do conjunto de caracteres aceitos pela linguagem, então o analisador léxico emitirá um erro. Já `massan` é composta por caracteres válidos e será reconhecida como um identificador, mesmo que esse identificador não faça sentido na gramática da linguagem — isso será tratado na próxima etapa (sintática).

Durante essa análise, alguns tokens **são gerados, mas depois descartados** em etapas posteriores, como **espaços em branco** e **comentários**. Esses elementos são geralmente **ignorados** no processo de tokenização, pois não influenciam diretamente na estrutura sintática, embora possam ser úteis para fins como formatação ou análise de estilo. 

> ⚠️ Obs: dizer que são "desprezados, mas não ignorados" é válido — pois o scanner pode reconhecer que eles existem, mas não os envia como tokens ao analisador sintático.



Após a identificação inicial (splitting), cada possível token passa por verificações:

1. **Verificação de Caracteres Inválidos:** O analisador confere se todos os caracteres dentro de um lexema pertencem ao alfabeto permitido pela linguagem. Por exemplo, a palavra `čachorro` contém um caractere inválido (`č`) que não faz parte do conjunto de caracteres aceitos pela maioria das linguagens de programação, então o analisador léxico emitirá um erro.

2. **Reconhecimento de Tipos:** Identifica se o token é uma palavra-chave, identificador, operador, literal, etc. `massan`, por exemplo, é composta por caracteres válidos e será reconhecida como um identificador, mesmo que esse identificador não faça sentido semântico ainda — isso será tratado em etapas posteriores (sintática e semântica).

3. **Tratamento de Stopwords (Contexto Específico):** Em alguns contextos de processamento de texto (mais comum em Processamento de Linguagem Natural, mas conceitualmente aplicável), pode haver uma etapa para identificar e potencialmente descartar "stopwords" – palavras muito comuns (como "o", "a", "de", "e") que podem não ser relevantes para certas análises. Em compiladores tradicionais, isso é menos comum para palavras-chave da linguagem, mas o conceito de filtrar tokens irrelevantes existe.

4. **Descarte de Irrelevantes:** Tokens como **espaços em branco** e **comentários** são geralmente reconhecidos pelo scanner, mas **descartados** e não enviados para a próxima fase (Análise Sintática), pois não afetam a lógica do programa diretamente.
    
    > ⚠️ Obs: dizer que são "desprezados, mas não ignorados" é válido — pois o scanner _reconhece_ que eles existem para separar outros tokens, mas não os repassa como tokens significativos.
    


### Estruturas de Dados Geradas

O Analisador Léxico geralmente produz ou interage com duas estruturas principais:

1. **Fila de Tokens:**
    
    - **Propósito:** Armazena a **sequência ordenada** por chegada de tokens significativos que foram reconhecidos no código-fonte. É a saída principal do analisador léxico e a entrada para o analisador sintático.
    - **Conteúdo:** Inclui tokens como palavras-chave, identificadores, operadores, literais e delimitadores importantes para a estrutura (como parênteses, chaves, ponto e vírgula). Separadores como espaços geralmente não entram aqui. Comentários entrariam se o compilador fosse especificado para linguagens de programação tradicionais. Mas como é uma linguagem natural, deve ser interessante inserir os comentários também.
    - **Exemplo:** Para `int x = 10;`, a fila seria `[TOKEN_INT, TOKEN_ID(x), TOKEN_ASSIGN, TOKEN_NUMBER(10), TOKEN_SEMICOLON]`. Se a entrada fosse `André André André`, a fila conteria três tokens representando "André".
2. **Tabela de Símbolos:**
    
    - **Propósito:** Armazena informações sobre os **identificadores** (nomes de variáveis, funções, classes, etc.) encontrados no código. O objetivo é manter um registro **único** de cada identificador e seus atributos (tipo, escopo, etc.), que serão usados nas fases sintática e semântica para verificar declarações, usos e consistência.
    - **Conteúdo:** Contém entradas únicas para cada identificador. Se `André` aparece 10 vezes, ele entra apenas uma vez na tabela de símbolos. Tokens que não são identificadores (como palavras-chave, operadores, números literais, delimitadores como `(`) geralmente **não entram** na tabela de símbolos principal, pois não são "nomes" a serem declarados ou referenciados dessa forma.
    - **Gerenciamento:**
        - **Verificação de Existência:** Antes de inserir um novo identificador, o analisador (ou a gestão da tabela) verifica se ele já existe.
        - **Similaridade e Formas Canônicas (Opcional/Avançado):** Em sistemas mais complexos ou voltados para linguagens naturais/correção, pode-se usar:
            - _Função de Similaridade:_ Para verificar se um novo identificador é muito parecido com um já existente (ex: corrigir `variavel` para `variável`). A complexidade dessa checagem pode ser O(n) se comparar com todos os 'n' existentes na tabela.
            - _Stemming/Forma Canônica:_ Armazenar apenas o radical da palavra ou a primeira forma encontrada como "canônica", mapeando variações para ela. Isso padroniza os identificadores na tabela.

O objetivo final desta fase é converter o fluxo de caracteres brutos em um fluxo estruturado de tokens (na Fila de Tokens) e começar a popular a Tabela de Símbolos com os identificadores encontrados, preparando o terreno para a análise da estrutura gramatical pelo Analisador Sintático.