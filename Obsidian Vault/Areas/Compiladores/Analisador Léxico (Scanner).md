
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