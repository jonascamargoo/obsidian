---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/arquitetura
criada: '2024-10-14'
---

## **Single Responsibility Principle**

- Uma classe deveria ter apenas um único motivo para mudar, foco na ;
- Classes/métodos/funções/módulos devem ter uma única responsabilidade bem definida: dicas para resolver é descrever tudo que o método faz, caso o nome fique muio grande, tem provavelmente mais de uma action
- segundo o **Princípio de Responsabilidade Única (SRP)**, uma classe deve ter um e apenas um motivo para ser alterada;

## **Open Closed Principle**

- Entidades de software (classes, módulos, funcs) devem estar sempre abertas para extensão, porém fechadas para modificação;
- cada classe deve conhecer e ser responsável por suas próprias regras de negócio;
- o princípio **Aberto/Fechado (OCP)** diz que um sistema deve ser aberto para a extensão, mas fechado para a modificação. Isso significa que devemos poder criar novas funcionalidades e estender o sistema sem precisar modificar muitas classes já existentes;
- Uma classe que tende a crescer "para sempre" é uma forte candidata a sofrer alguma espécie de refatoração.


## Liskov substitution principle

	- Se criarmos uma subclasse B de uma classe A, utilizando herança, o Objeto instanciado da classe B tem de conseguir substituir o objeto da classe pai (A), ilustração: Considerando a classe pai responsável por fazer café, na situação certa, a filha deveria ser possibilitada de fazer um cappuccino por exemplo (ainda é um café). Na situação errada, ele diria que n sabe fazer café igual o pai, mas sabe fazer coisa melhor (whiskey). Ta errado.

#### Why?

Respeitar o princípio força o programa de ter abstrações no nível certa e ser mais consistente. Exemplo:

```class Ave() {
	void bicar(){...}
	void voar(){...}
}
```

Se a subclasse for PicaPau, ok, pois ele corresponde a ambas actions, mas e class Pinguim extends Ave? Vai ter problema, a abstração ta errada. Portanto, devemos perceber isso o quanto antes e evitar problemas piores.

## Interface segregation principle

Clientes (nesse caso, classes) não devem ser forçados a implementar interfaces com métodos que elas não irão utilizar.  Se eu tenho:

```interface ataque {
	bica()
	nada()
	voaEBica()
}
```

uma classe Pinguim não poderia implementar a interface ataque, pois teria que achar outra solução para implementar o VoaEBica, por nao voar, e por ai vai... O segredo é manter as interfaces segregadas


## Dependency inversion principle

Um módulo não deve depender de detalhes de implementação de outro módulo DIRETAMENTE. Deve existir uma abstração (talvez uma interface) entre eles. Exemplo: um cortador de pizza não deveria precisar de uma ferramenta que corta pizza, ele deveria precisar de uma ferramenta qualquer. A ferramenta que  se encaixar nos requisitos da interface, consegue ser utilizado. Esse princípio nada mais é que o produto do uso rigoroso dos open close principle & liskov subs prin. 
