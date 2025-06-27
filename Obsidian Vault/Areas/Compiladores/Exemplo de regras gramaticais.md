## Contexto

Forneça para a disciplina de Compiladores a sua definição gramatical (em gramática formal BNF, por qualquer notação) da linguagem natural mobilizada pelo usuário para envio a um search engine que aceite linguagem natural.

Sua linguagem basicamente precisa ter regras gramaticais para textos (perguntas, em que o usuário pede ajuda ao search engine e respostas, em que o usuário indica algo que o search engine pediu), sobre documentos eletrônicos.

Neste momento, sua gramática precisa fornecer pelo menos cinco regras gramaticais para perguntas do usuário para o search engine e pelo menos cinco regras gramaticais para respostas do usuário para o search engine (sempre é do usuário, ok?! Não são respostas do próprio search engine).


Exemplos de perguntas:

```
Qual documento está no <formato>?

Qual tamanho tem <formato>?

Qual documento tem <titulo>?

  

Exemplos de atribuição:

O formato é <formato>.

Quero tamanho maior que <numero>.

```

## Implementação

```
<interacao_usuario> ::= <pergunta> | <resposta_usuario>

// --- REGRAS PARA PERGUNTAS DO USUÁRIO ---

<pergunta> ::= <pergunta_sobre_atributo_documento>
            | <pergunta_sobre_existencia_documento>
            | <pergunta_sobre_contagem_documento>
            | <pergunta_sobre_localizacao_documento>
            | <pergunta_sobre_conteudo_documento>

<pergunta_sobre_atributo_documento> ::= <palavra_interrogativa> <substantivo_documento> <verbo_estar_ter> <preposicao_em_de_com> <termo_atributo> "?"
                                    | <palavra_interrogativa> <termo_atributo_singular> <verbo_ter_possuir> [<artigo_definido_singular>] <substantivo_documento> <identificador_documento> "?"
                                    | <palavra_interrogativa> <substantivo_documento_plural> <verbo_possuir_plural> <termo_atributo> <valor_atributo> "?"

<pergunta_sobre_existencia_documento> ::= <palavra_interrogativa> <substantivo_documento> <verbo_ter_possuir> <termo_titulo> <valor_titulo> "?"
                                     | <verbo_existir_haver_interrogativo> <substantivo_documento> <preposicao_com_de> <termo_formato> <valor_formato> "?"

<pergunta_sobre_contagem_documento> ::= <palavra_interrogativa_quantitativa> <substantivo_documento_plural> <verbo_existir_haver_plural> [<preposicao_em_de_com> <termo_formato> <valor_formato>] "?"

<pergunta_sobre_localizacao_documento> ::= <palavra_onde> <verbo_estar> <substantivo_documento> <identificador_documento> "?"

<pergunta_sobre_conteudo_documento> ::= <palavra_interrogativa> <substantivo_documento> <verbo_conter_falar> <preposicao_sobre_de> <termo_palavra_chave> <valor_palavra_chave> "?"


// --- REGRAS PARA RESPOSTAS/ATRIBUIÇÕES DO USUÁRIO ---

<resposta_usuario> ::= <atribuicao_de_formato>
                    | <atribuicao_de_tamanho>
                    | <atribuicao_de_titulo>
                    | <atribuicao_de_data>
                    | <atribuicao_de_palavra_chave_resposta>

<atribuicao_de_formato> ::= [<artigo_definido_singular>] <termo_formato> <verbo_ser_singular> <valor_formato> "."
                         | <pronome_preferencia> <termo_formato> <valor_formato> "."

<atribuicao_de_tamanho> ::= <pronome_preferencia> <termo_tamanho> <comparador_tamanho> <valor_numerico> [<unidade_tamanho>] "."
                         | [<artigo_definido_singular>] <termo_tamanho> <verbo_ser_singular> <preposicao_de> <valor_numerico> [<unidade_tamanho>] "."

<atribuicao_de_titulo> ::= [<artigo_definido_singular>] <termo_titulo> <verbo_ser_singular> <valor_titulo> "."
                        | <pronome_busca_filtro> <substantivo_documento> <preposicao_com_de> <termo_titulo> <valor_titulo> "."

<atribuicao_de_data> ::= <pronome_preferencia> <substantivo_documento_plural> <verbo_ser_plural_modificado_por_data> <preposicao_de_apos_antes> <valor_data> "."
                      | [<artigo_definido_singular>] <termo_data_criacao_modificacao> <verbo_ser_singular> <valor_data> "."

<atribuicao_de_palavra_chave_resposta> ::= <pronome_interesse> <preposicao_em_por> <substantivo_documento_plural> <verbo_conter_plural> <termo_palavra_chave> <valor_palavra_chave> "."


// --- COMPONENTES LÉXICOS E GRUPOS MENORES (NÃO TERMINAIS AUXILIARES) ---

<palavra_interrogativa> ::= "Qual" | "Quais" | "Que"
<palavra_interrogativa_quantitativa> ::= "Quantos" | "Quantas"
<palavra_onde> ::= "Onde"

<substantivo_documento> ::= "documento" | "arquivo" | "ficheiro" | "item"
<substantivo_documento_plural> ::= "documentos" | "arquivos" | "ficheiros" | "itens"

<verbo_estar_ter> ::= "está" | "tem" | "possui" | "encontra-se"
<verbo_ter_possuir> ::= "tem" | "possui"
<verbo_possuir_plural> ::= "têm" | "possuem"
<verbo_estar> ::= "está" | "se encontra" | "localiza-se"
<verbo_existir_haver_interrogativo> ::= "Existe" | "Há"
<verbo_existir_haver_plural> ::= "existem" | "há"
<verbo_conter_falar> ::= "contém" | "fala" | "trata" | "menciona"
<verbo_conter_plural> ::= "contenham" | "falem" | "tratem" | "mencionem"

<verbo_ser_singular> ::= "é" | "seja"
<verbo_ser_plural_modificado_por_data> ::= "criados" | "modificados" | "acessados" // Adjetivos verbais

<preposicao_em_de_com> ::= "no" | "em" | "do" | "de" | "com" | "pelo" | "na" | "da" | "pela"
<preposicao_sobre_de> ::= "sobre" | "de" | "acerca de"
<preposicao_de_apos_antes> ::= "de" | "após" | "depois de" | "antes de"
<preposicao_em_por> ::= "em" | "por"

<artigo_definido_singular> ::= "o" | "a"

<termo_atributo> ::= <termo_formato> | <termo_tamanho> | <termo_titulo> | <termo_data_criacao_modificacao> | <termo_nome_arquivo>
<termo_atributo_singular> ::= "formato" | "tamanho" | "título" | "nome" | "data de criação" | "data de modificação"

<termo_formato> ::= "formato" | "extensão" | "tipo"
<termo_tamanho> ::= "tamanho" | "espaço"
<termo_titulo> ::= "título" | "nome" | "denominação"
<termo_data_criacao_modificacao> ::= "data de criação" | "data de modificação" | "data"
<termo_nome_arquivo> ::= "nome de arquivo" | "nome do arquivo"
<termo_palavra_chave> ::= "palavra-chave" | "termo" | "assunto" | "tag"

<identificador_documento> ::= <valor_generico> // Pode ser um nome, ID, etc.

<valor_atributo> ::= <valor_formato> | <valor_titulo> | <valor_numerico>
<valor_formato> ::= "<formato>" // Ex: ".pdf", ".docx", "texto"
<valor_titulo> ::= "<titulo>"   // Ex: "Relatório Anual", "Tese Final"
<valor_palavra_chave> ::= "<palavra_chave>" // Ex: "inteligência artificial", "compiladores"
<valor_data> ::= "<data>" // Ex: "DD/MM/YYYY", "hoje", "ontem", "última semana"
<valor_numerico> ::= "<numero>" // Ex: "10", "25.5"
<unidade_tamanho> ::= "KB" | "MB" | "GB" | "bytes"

<pronome_preferencia> ::= "Quero" | "Gostaria de" | "Prefiro" | "Desejo"
<pronome_busca_filtro> ::= "Busque por" | "Filtre por" | "Encontre"
<pronome_interesse> ::= "Estou interessado" | "Tenho interesse"

<comparador_tamanho> ::= "maior que" | "menor que" | "igual a" | "entre" <valor_numerico> "e"

<valor_generico> ::= /["\w\s.-]+/ // Sequência de caracteres alfanuméricos, espaços, pontos, hífens

```

