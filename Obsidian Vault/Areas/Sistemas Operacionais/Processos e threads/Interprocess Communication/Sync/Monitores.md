
Com semáforos e mutexes, a comunicação entre processos parece fácil, certo? Errado. Observe de perto a ordem dos downs antes de inserir ou remover itens do buffer na Figura 2.28. Suponha que os dois downs no código do produtor fossem invertidos, de maneira que mutex tenha sido decrescido antes de empty em vez de depois dele. Se o buffer estivesse completamente cheio, o produtor seria bloqueado, com mutex configurado para 0. Em consequência, da próxima vez que o consumidor tentasse acessar o buffer, ele faria um down em mutex, agora 0, e seria bloqueado também. Ambos os processos ficariam bloqueados para sempre e nenhum trabalho seria mais realizado. Essa situação infeliz é chamada de **impasse** (_deadlock_). Estudaremos impasses detalhadamente no Capítulo 6.

### Algumas chamadas de Pthreads relacionadas a mutexes:

- `pthread_mutex_init`: Cria um mutex
- `pthread_mutex_destroy`: Destrói um mutex existente
- `pthread_mutex_lock`: Obtém uma trava ou é bloqueado
- `pthread_mutex_trylock`: Obtém uma trava ou falha
- `pthread_mutex_unlock`: Libera uma trava

### Algumas das chamadas de Pthreads relacionadas com variáveis de condição:

- `pthread_cond_init`: Cria uma variável de condição
- `pthread_cond_destroy`: Destrói uma variável de condição
- `pthread_cond_wait`: Bloqueia esperando por um sinal
- `pthread_cond_signal`: Sinaliza para outro thread e o desperta
- `pthread_cond_broadcast`: Sinaliza para múltiplos threads e desperta todos eles

---

### Código exemplo usando threads para solucionar o problema produtor-consumidor:

```
#include <stdio.h>
#include <pthread.h>
#define MAX 1000000000 /* quantos números produzir */

pthread_mutex_t the_mutex;
pthread_cond_t condc, condp; /* usado para sinalização */
int buffer = 0; /* buffer usado entre produtor e consumidor */

void *producer(void *ptr) {
    int i;
    for (i = 1; i <= MAX; i++) {
        pthread_mutex_lock(&the_mutex); /* obtém acesso exclusivo ao buffer */
        while (buffer != 0) pthread_cond_wait(&condp, &the_mutex);
        buffer = i; /* coloca item no buffer */
        pthread_cond_signal(&condc); /* acorda consumidor */
        pthread_mutex_unlock(&the_mutex); /* libera acesso ao buffer */
    }
    pthread_exit(0);
}

void *consumer(void *ptr) {
    int i;
    for (i = 1; i <= MAX; i++) {
        pthread_mutex_lock(&the_mutex); /* obtém acesso exclusivo ao buffer */
        while (buffer == 0) pthread_cond_wait(&condc, &the_mutex);
        buffer = 0; /* retira o item do buffer */
        pthread_cond_signal(&condp); /* acorda o produtor */
        pthread_mutex_unlock(&the_mutex); /* libera acesso ao buffer */
    }
    pthread_exit(0);
}

int main(int argc, char **argv) {
    pthread_t pro, con;
    pthread_mutex_init(&the_mutex, 0);
    pthread_cond_init(&condc, 0);
    pthread_cond_init(&condp, 0);
    pthread_create(&con, 0, consumer, 0);
    pthread_create(&pro, 0, producer, 0);
    pthread_join(pro, 0);
    pthread_join(con, 0);
    pthread_cond_destroy(&condc);
    pthread_cond_destroy(&condp);
    pthread_mutex_destroy(&the_mutex);
}


```


Esse problema é destacado para mostrar o quão cuidadoso você precisa ser ao usar semáforos. Um erro sutil e tudo para completamente. É como programar em linguagem de montagem, mas pior, pois os erros envolvem **condições de corrida**, **impasses** e outras formas de comportamento imprevisível e irreproduzível.

Para facilitar a escrita de programas corretos, **Brinch Hansen** (1973) e **Hoare** (1974) propuseram uma primitiva de sincronização de nível mais alto chamada **monitor**. Um **monitor** é uma coleção de rotinas, variáveis e estruturas de dados que são reunidas em um tipo especial de módulo ou pacote. Processos podem chamar as rotinas em um monitor sempre que eles quiserem, mas eles não podem acessar diretamente as estruturas de dados internas do monitor a partir de rotinas declaradas fora dele.

Monitores têm uma propriedade importante que os torna úteis para realizar a exclusão mútua: **apenas um processo pode estar ativo em um monitor em qualquer dado instante**.