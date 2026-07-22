---
tipo: conceito
area: Sistemas Operacionais
tags:
- so
criada: '2025-01-21'
---

Quando ocorre uma page fault, o SO **precisa** escolher uma página para remover da memória, para abrir espaço para outra. Há o caso em que, enquanto estava em memória, a página ter sido modificada (dai precisa ser realocada, carregando o dado atual para o disco) e existe o caso em que ela não foi alterada, podendo apenas ser sobreescrita.

