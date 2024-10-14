# Flexbox

## Flex tips

- O display flex deve ser adicionado ao elemento pai, para que ocorra a fluidez nos elementos filhos
- Poderemos utilizar o align-items: center para colocar os elementos em mesmo nível vertical;
- Justify-content - podemos distribuir os elementos dentro do pai de diversas formas, podemos por exemplo:
    - Colocar todo espaço à esquerda, jogando o conteúdo para direita com `justify-content: flex-end;`
    - Colocar todo espaço à direita, jogando o conteúdo para esquerda com `justify-content: flex-start` (que é o padrão);
    - Colocar todo espaço à esquerda e à direita, jogando o conteúdo para o meio com `justify-content: center;`
    - Colocar todo espaço entre os elementos como vimos antes usando `justify-content: space-between;`
- Para dispor os elementos verticalmente deveremos setar o space flex-direction: column e para evitar que fique fora de formatação e saia de dentro do container pai, setaremos o flex-wrap: wrap. OOOOU podemos utilizar o flex-flow: column wrap; que substitui esses dois últimos! Separar o elemento filho pela widith percent. Ou seja, se tiver 5 elementos, width: 20%. Se tiver 4: width: 25%
- Por que às vezes pode ser complicado utilizar `justify-content: space-between`
 ou `space-around`
 para o grid?  (grid são vários link listados. Tipo a pag “meus cursos” da alura
    - É complicado utilizá-las porque elas colocam comportamentos que não são legais para grids, por exemplo, se utilizarmos `space-around`/between
     e na última linha do grid tivermos apenas dois itens ao invés de quatro, o espaçamento entre eles vai ficar feio.
    - GRID tratando listas
        - Podemo utilizar o .class:nth-child(4n) para tratar do quarto elemento de um lista. Ou .class:nth-child(4n+1) {}, pois a contagem começa do zero, primeiro elemento da lista é posição 0.
        - **Como espaçar corretamente os elementos de um grid:**
            
            ```
            <div class="grid">
            
              <!-- primeira linha -->
              <div class="course"></div>
              <div class="course"></div>
              <div class="course"></div>
            
              <!-- segunda linha -->
              <div class="course"></div>
              <div class="course"></div>
              <div class="course"></div>
            
            </div>
            ```
            
            ```
            .grid {
              display: flex;
              flex-wrap: wrap;
            }
            
            .course {
              width: 31.3%;
              margin: 1%;
            }
            ```
            

- Inversão de eixos
    - quando mudamos a flex direction , os eixos mudam. Logo, align item muda do alinhamento vertical para o horizontal, por exemplo. Justify-content vai mudar do eixo x para o y (colocar espaço se tiver espaço)