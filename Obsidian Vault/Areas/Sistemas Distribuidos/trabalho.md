Um modelo cliente servidor que não é de conectivdade direta (via ip), talvez por DNS. O sistema distribuído é basicamente um servidor http, ele não tem informações de qual item ele tá acessando (se é a home em cacche de um site, se é outra notícia  irrelevante a qual não ficaria em cache).  Os componentes (Sistema distribuído, sistema operacional de rede e a rede em si) são desacoplados. Quem defini se aquele conteúdo está em cache ou disco é o sistema operacional de rede.


SD1-> SOR2 -> rede -> SOR2 -> SD2


### 5.3. Nota sobre o Trabalho 1
**Foco do trabalho:** Entender a parte transacional entre cliente e servidor. Estudar as soluções dos exercícios propostos.