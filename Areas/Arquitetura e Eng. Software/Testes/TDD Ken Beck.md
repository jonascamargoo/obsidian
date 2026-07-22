---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/testes
criada: '2024-10-14'
---

## O que é?

1. Escreva um teste rapidamente;
2. Rodar todos os testes e ver o mais novo falhando (faça-o compilar);
	1. . utilizando stubs, mocks, anyway, os testes precisam compilar
3. Rode-o e veja-o falhar
4. Rodar todos os testes e ver todos funcionando.
5. Refatorar para remover duplicações.

	As diferentes fases têm diferentes propósitos. Elas invocam estilos diferentes de solução, diferentes perspectivas estéticas. As primeiras três fases precisam passar rapidamente, assim chegamos a um estado conhecido com a nova funcionalidade. Podemos cometer qualquer número de pecados para chegar lá, pois a velocidade agora é melhor que o projeto, ao menos por um breve momento.
## O que percebemos ao aplicar?

- Como cada teste pode cobrir um pequeno aumento de funcionalidade;
- Quão pequenas e feias as mudanças podem ser para fazer os novos testes rodarem;
-  Com frequência os testes são executados;
- De quantos pequeninos passos as refatorações são compostas;
- Redução do escopo (antes precisávamos que a feature fizesse algo abstrato, agora só precisamos fazer o teste funcionar);

#### De forma mais detalhada

	1. Escreva um teste. Pense em como você gostaria que a operação em sua mente aparecesse em seu código. Você está escrevendo uma história. Invente a interface que deseja ter. Inclua na história todos os elementos que você imagina que serão necessários para calcular as respostas certas.
	
	3. Faça-o rodar. Fazer rapidamente aquela barra ir para verde domina todo o resto. Se a solução limpa e simples é óbvia, então codifique-a. Se a solução limpa e simples é óbvia, mas vai levar um minuto, então tome nota dela e volte para o problema principal que é deixar a barra verde em segundos. Essa mudança na estética é difícil para alguns engenheiros de software experientes. Eles apenas sabem como seguir as regras da boa engenharia. Um verde rápido perdoa todos os pecados. Mas, apenas por um momento.
	
	4. Faça direito. Agora que o sistema está se comportando, ponha os caminhos pecaminosos do passado recente atrás de você. Dê um passo para trás na correta e minuciosa trilha da integridade de software. Remova a duplicação que você introduziu e chegue ao verde rapidamente.


## Os 3 estilos de se aplicar o TDD

### Estratégia 1: Engane-o (Fake It)

- **Descrição**: Comece retornando uma constante fixa em vez de uma implementação completa e correta. Gradualmente, substitua essas constantes por variáveis e lógica real até que o código esteja implementado corretamente.
- **Exemplo**: Se você está escrevendo uma função para somar dois números, inicialmente, você pode apenas retornar um valor fixo que faça o teste passar.

	```python
def soma(a, b):
    return 42 # Retorna uma constante fixa para passar o teste inicial
```

- **Aplicação**: À medida que você adiciona mais testes e refina a função, você começa a substituir a constante fixa por uma lógica que manipula os parâmetros reais.

```python
def soma(a, b):
    return a + b # Substitua a constante fixa pela lógica correta
```

### Estratégia 2: Implementação Óbvia (Obvious Implementation)

- **Descrição**: Quando você sabe exatamente como deve ser a implementação correta, codifique-a diretamente.
- **Exemplo**: Se a tarefa é simples e você tem certeza da solução, escreva a implementação real desde o início.

```python
def soma(a, b):
    return a + b # Implementação real desde o início
```

### Estratégia 3: Triangulação

**triangulação** é uma estratégia onde você escreve vários testes diferentes que cobrem diversos casos para uma mesma funcionalidade.  Se duas estações receptoras, situadas a uma distância conhecida uma da outra, conseguem medir a direção de um sinal de rádio, então é possível calcular tanto a distância quanto a direção do sinal. Esse cálculo, conhecido como Triangulação, requer conhecimentos de trigonometria.

Em vez de fazer uma implementação generalizada de uma vez, você implementa a funcionalidade de forma incremental, baseada nos resultados de múltiplos testes. Isso ajuda a garantir que a implementação é correta e cobre uma variedade de cenários.

``` java
public void testEquality() {
	assertTrue(new Dollar(5).equals(new Dollar(5)));
	assertFalse(new Dollar(5).equals(new Dollar(6)));
}
```

Agora sim, podemos generalizar o código. OBS: triangulação é uma estratégia de toral insegurança
### Abordagem Combinada da estrategia 1 e 2

**Alternância entre Estratégias**: Na prática, ao usar TDD, o desenvolvedor pode alternar entre essas duas estratégias com base na confiança e clareza sobre a solução.
    - **Implementação Óbvia**: Quando você tem certeza de como implementar a funcionalidade e sabe que ela passará nos testes, use a Implementação Óbvia.
    - **Engane-o**: Quando surge uma incerteza ou você recebe um erro inesperado (barra vermelha), mude para a estratégia Engane-o. Isso permite avançar gradualmente enquanto ainda mantém os testes passando.

**Ciclo de Confiança e Refatoração**:

- **Confiança Alta**: Quando a confiança está alta e você entende bem o problema, escreva Implementações Óbvias seguidas de testes para garantir que sua compreensão está correta.
- **Confiança Baixa**: Ao encontrar um problema ou erro inesperado, mude para uma implementação falsa (Engane-o). Isso ajuda a isolar e entender o problema sem a pressão de fazer tudo funcionar de imediato.
- **Recuperação da Confiança**: Uma vez que o problema é resolvido ou entendido melhor, volte a usar Implementações Óbvias.



## Considerações

1 - TDD anda lado a lado com imutabilidade. A utilização de value object é bastante corriqueira
2 - Traduzir um sentimento, sobre como o sistema deveria funcionar para, para um teste é um dos pontos principais do TDD. Isso contribui a entender de fato o funcionamento do sistema vigente. 