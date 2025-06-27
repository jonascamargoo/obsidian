## O que são documentos no contexto computacional

**Um documento, no contexto da computação, é uma coleção nomeada de dados digitais, tratada como uma unidade lógica pelo sistema computacional, e que é obrigatoriamente associada a um conjunto de metadados descritivos e de gerenciamento. Esses metadados incluem, no mínimo:**

1. **Nome (Identificador):** Um nome único (dentro de seu contexto, como um diretório) que permite ao sistema operacional e aos usuários referenciar o documento.
2. **Datas/Horários (Timestamps):**
    - **Data de Criação:** O momento em que o documento foi inicialmente criado no sistema.
    - **Data de Modificação (ou Alteração):** O momento da última vez que o conteúdo do documento foi alterado e salvo.
    - **Data de Acesso (opcional, mas comum):** O momento da última vez que o documento foi lido ou acessado.
3. **Tipo/Formato:** Informação que indica a natureza dos dados contidos (ex: .txt, .jpg, .pdf, .docx), permitindo que o sistema ou aplicativos saibam como interpretá-los.
4. **Tamanho:** A quantidade de dados que o documento contém, geralmente medida em bytes.
5. **Atributos de Sistema/Controle:**
    - **Localização:** Informações sobre onde os dados do documento estão fisicamente ou logicamente armazenados (ex: caminho no sistema de arquivos, ponteiros para blocos de dados).
    - **Permissões de Acesso:** Regras que definem quem pode ler, escrever, executar ou modificar o documento (ex: proprietário, grupo, outros).
    - **Proprietário/Criador:** Identificação do usuário ou processo que criou ou possui o documento.

**Contextualização e Importância:**

- **Sistema de Arquivos:** A maioria dos sistemas operacionais utiliza uma estrutura chamada **inode** (em sistemas Unix-like) ou conceitos equivalentes (como entradas na Master File Table - MFT no NTFS do Windows) para armazenar esses metadados. O inode é uma estrutura de dados que contém todas essas informações _sobre_ o arquivo, exceto o seu nome (que geralmente é armazenado na estrutura do diretório) e o próprio conteúdo de dados (que é apontado pelo inode).
- **Gerenciamento de Documentos:** Em sistemas de gerenciamento eletrônico de documentos (GED/ECM), a quantidade e a sofisticação dos metadados associados a um documento são ainda maiores, incluindo versões, status do fluxo de trabalho, palavras-chave, categorias, datas de expiração, etc.
- **Integridade e Rastreabilidade:** Esses metadados são fundamentais para a organização, busca, recuperação, segurança, controle de versão e auditoria de documentos em um ambiente computacional. Eles fornecem o contexto necessário para que o "saco de bits" que compõe o conteúdo do documento se torne uma informação útil e gerenciável.
## BNF

BNF stands for **Backus Naur Form** notation. It is a formal method for describing the syntax of programming language which is understood as Backus Naur Formas introduced by John Bakus and Peter Naur in 1960. BNF and [CFG (Context Free Grammar)](https://www.geeksforgeeks.org/classification-of-context-free-grammars/) were nearly identical. BNF may be a meta-language (a language that cannot describe another language) for primary languages. 

For human consumption, a proper notation for encoding grammars intended and called Backus Naur Form (BNF). Different languages have different description and rules but the general structure of BNF is given below – 

name ::= expansion

The symbol ::= means “may expand into” and “may get replaced with.” In some texts, a reputation is additionally called a non-terminal symbol. 

- Every name in Backus-Naur form is surrounded by angle brackets, < >, whether it appears on the left- or right-hand side of the rule. 
    
- An expansion is an expression containing terminal symbols and non-terminal symbols, joined together by sequencing and selection. 
    
- A terminal symbol may be a literal like (“+” or “function”) or a category of literals (like integer). 
    
- Simply juxtaposing expressions indicates sequencing. 
    
- A vertical bar | indicates choice. 
    
    **Examples :**  
    

<expr> ::= <term> "+" <expr>
        |  <term>

<term> ::= <factor> "*" <term>
        |  <factor>

<factor> ::= "(" <expr> ")"
          |  <const>

<const> ::= integer

**Rules For making BNF :**   
Naturally, we will define a grammar for rules in BNF –   
 

rule → name ::= expansion
name → < identifier >
expansion → expansion expansion
expansion → expansion | expansion
expansion → name
expansion → terminal

- We might define identifiers as using the regular expression [-A-Za-z_0-9]+. 
    
- A terminal could be a quoted literal (like “+”, “switch” or ” “<<=”) or the name of a category of literals (like integer). 
    
- The name of a category of literals is typically defined by other means, like a daily expression or maybe prose. 
    
    It is common to seek out regular-expression-like operations inside grammars. as an example, the Python lexical specification uses them. In these grammars:   
     
    

postfix * means "repeated 0 or more times"
postfix + means "repeated 1 or more times"
postfix ? means "0 or 1 times"

The definition of floating-point literals in Python may be an exemplar of mixing several notations – 

floatnumber   ::=  pointfloat | exponentfloat
pointfloat    ::=  [intpart] fraction | intpart "."
exponentfloat ::=  (intpart | pointfloat) exponent
intpart       ::=  digit+
fraction      ::=  "." digit+
exponent      ::=  ("e" | "E") ["+" | "-"] digit+

It does not use angle brackets around names (like many EBNF notations and ABNF), yet does use ::= (like BNF). It mixes regular operations like + for non-empty repetition with EBNF conventions like [ ] for option. The grammar for the whole Python language uses a rather different (but still regular) notation.