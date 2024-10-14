
Chamando função assembly em código C.

Criando o assembly:

```assembly
.text
.global func

func:
  pushl %ebp
  movl %esp, %ebp
  subl $0, %esp
  movl $10, %eax
  movl %ebp, %esp
  popl %ebp
ret
```

Chamando em C:

```c
#include <stdio.h>

int main()

{
 printf(""%d\n", res");
}

```


Compilando

```bash
gcc -m32 simples.s simples.c -o simples
```

o GNU Compiler Collection (gcc) compila e linka o código assembly e C a um executável final chamado "simples". O -m32 foi para executar um assembly 32 em uma máquina 64





