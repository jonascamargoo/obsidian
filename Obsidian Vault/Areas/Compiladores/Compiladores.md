## O que é um compilador?

Um **compilador** é um **tradutor automático** que converte um código-fonte escrito em uma **linguagem de alto nível** (como C, Java, Python) para uma **linguagem de baixo nível**, como **linguagem de máquina** ou **bytecode**. O objetivo é permitir que o código seja **executado por um computador**. Também é possível realizar o processo inverso, informalmente chamado de "decompilação". 

Mas compiladores **não se limitam a linguagens de programação**! Ferramentas como o **Google Tradutor** e o recurso de **sugestões automáticas do Google Docs** também utilizam conceitos de compilação (traduzindo de português para português, por exemplo) . Eles traduzem de uma linguagem (como o português) para outra (como o inglês), passando por etapas semelhantes: análise léxica, sintática, semântica e geração de resultado.

No senso comum entre profissionais de computação, um **compilador** é um software que **transforma código-fonte**, escrito em uma **linguagem de programação de alto nível**, em **código de máquina** que pode ser executado diretamente por um processador.

Mas compilar **vai além** de apenas traduzir código. O processo é dividido em várias etapas, nas quais o compilador **analisa, interpreta, otimiza e gera instruções** adequadas para o computador, garantindo que o programa seja não só **executável**, mas também **eficiente e portátil**.

#### Por que compiladores são importantes?

- Permitem programar de forma **abstrata**, sem se preocupar com o hardware.
    
- Tornam o software **portátil**, funcionando em diferentes plataformas.
    
- Realizam **otimizações** que melhoram o desempenho do código.
    
- Ajudam a identificar **erros estáticos**, ainda na fase de compilação.
    
- São usados **além de linguagens de programação**, como em linguagens naturais.

## Etapas do Compilador


1. lexico
2. sintático
	.
	.
	.

Quanto **mais aberta** (ambígua ou flexível) for uma linguagem, especialmente linguagens naturais, **menos rígida será a análise léxica**, e **mais trabalho será repassado ao analisador sintático**. Isso acontece porque o léxico foca apenas na formação de tokens, enquanto o parser precisa lidar com ambiguidade e estrutura gramatical.






---
INSERIR AQUI AS FASES

LEMBRAR DE FALAR QUE O INTERPRETADOR JAVA ACEITA UMA ÁRVORE

INSERIR AS FOTOS E UTILIZAR O MESMO EXEMPLO




## 🆚 Compilação vs Interpretação

Ambos os processos — **compilação** e **interpretação** — têm o objetivo de **executar programas escritos em linguagens de alto nível**, mas eles o fazem de formas bem diferentes.

---

### 🛠️ **Compilação**

Um **compilador** é um software que **lê todo o código-fonte de uma vez**, analisa, transforma e **gera um novo programa**, normalmente em **código de máquina** ou **código intermediário**, como assembly.

📌 Durante a compilação:

1. O código-fonte é lido por completo.
    
2. Passa pelas etapas: **análise léxica**, **sintática**, **semântica**, **otimizações**, e por fim a **geração de código**.
    
3. O resultado final é um **arquivo executável** (ex: `.exe`, `.out`), que pode ser rodado diretamente pelo sistema operacional, sem precisar do código-fonte ou do compilador mais.

📌 **Detalhe importante:**  
O compilador percorre a **árvore sintática abstrata (AST)** do programa e, a partir dela, **gera uma árvore equivalente em linguagem de baixo nível**, como **assembly**. Essa árvore contém instruções que serão posteriormente traduzidas para **binário**.

## 🧠 Importante: Linguagens não são compiladas ou interpretadas por natureza!

É comum ouvir frases como _"C é uma linguagem compilada"_ ou _"Python é uma linguagem interpretada"_, mas **isso não está tecnicamente correto**.

A verdade é:

> 🔹 **Linguagens de programação não são compiladas nem interpretadas — elas são apenas especificações de sintaxe e semântica.**  
> 🔹 O que é compilado ou interpretado é a **implementação do compilador ou interpretador** daquela linguagem.

---

### 📌 Exemplo prático:

- O **C** é tradicionalmente implementado por compiladores como o `gcc`, que geram código de máquina.
    
- O **Python** é comumente interpretado pelo **CPython**, mas também pode ser **compilado** com ferramentas como **Cython** ou **PyPy (com JIT)**.
    
- O **JavaScript**, tradicionalmente interpretado em navegadores, hoje é **compilado just-in-time (JIT)** por engines como o V8 (Google Chrome).
    

Então, dizer que "C é compilado" e "Python é interpretado" **reflete o uso mais comum**, mas não é tecnicamente preciso. Geralmente, o mantenedor principal detém essa decisão.














APAGAR ISSO DEPOIS
### Considerações Adicionais

- **Comentário**: Comentários são removidos já na etapa léxica. Eles não viram tokens e não chegam ao analisador sintático.
    
- **Espaços e delimitadores**: Tokens como espaço em branco e `;` (ponto e vírgula) podem ser tratados de forma especial. O ponto e vírgula, por exemplo, **pode ser necessário** para o parser entender o fim de uma instrução, enquanto espaços são geralmente ignorados.
    
- **Gazetteer**: Um _gazetteer_ (dicionário geográfico) é usado em linguagens naturais para associar palavras a lugares geográficos. Em NLP (Processamento de Linguagem Natural), pode ser usado na análise semântica. Embora não esteja diretamente ligado a compiladores tradicionais, faz sentido mencionar isso se você estiver comparando com a análise de linguagens naturais.

---




