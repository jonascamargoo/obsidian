---
curso: DDI Associate
aula: 9
titulo: "Explore More: Dicas para Nomear seus Computadores"
fonte: Infoblox Education
duracao: 1m
dificuldade: Beginner
tags:
  - DDI
  - DNS
  - hostname
  - boas-praticas
  - RFC1178
  - explore-more
data: 2026-05-28
---

# Aula 9 — Explore More: Dicas para Nomear seus Computadores

> [!info] Resumo
> Escolher um **hostname** é o primeiro passo ao configurar uma máquina. Convenção de nomes é um problema tão antigo quanto o próprio DNS — **não reinvente a roda**: aprenda com o que outros já tentaram e evite seus erros. O **RFC 1178** reúne boas práticas, com uma mensagem central: **mantenha os nomes simples e claros**.

---

## 📘 RFC 1178 — Boas práticas de nomenclatura

Não é um livro de regras rígidas, mas um conjunto de **boas práticas** focado em **evitar problemas**. As principais:

- **Mantenha curto** 🔡
  - Nomes longos são difíceis de digitar e fáceis de errar.
- **Evite nomes "espertos"/confusos** 🤔
  - Fuja de palavras como *"up"* ou *"down"*, que confundem em conversas ou na rede.
- **Pule caracteres especiais** ✂️
  - Use apenas **letras, números e traços (dashes)**.
  - **Não presuma** que o software distingue **maiúsculas de minúsculas**.

---

## 🗂️ Três estratégias comuns de nomenclatura

### 1. Nomenclatura Descritiva
- Abordagem **mais comum em ambientes profissionais**.
- O nome diz **exatamente o que o computador é e o que faz**.
- Ex.: o servidor web principal de uma empresa → `web-server-prod-01`.
- **Eficiente** para gerenciar **grandes redes**.

### 2. Nomenclatura Temática
- Método **divertido e popular** para redes domésticas ou projetos pessoais.
- Escolhe-se um **tema** (planetas, deuses gregos, personagens de filme) e nomeiam-se todas as máquinas dentro dele.
- Ex.: `jupiter`, `mars`, `venus`.

### 3. Nomenclatura Aleatória
- Para sistemas **muito grandes e automatizados**.
- Os computadores recebem nomes **aleatórios**, como `vm-1a52`.
- Deixa claro que o nome é apenas um **identificador único**, não uma descrição da função.

| Estratégia | Melhor para | Exemplo |
|-----------|-------------|---------|
| **Descritiva** | Ambientes profissionais / grandes redes | `web-server-prod-01` |
| **Temática** | Redes domésticas / projetos pessoais | `jupiter`, `mars`, `venus` |
| **Aleatória** | Sistemas grandes e automatizados | `vm-1a52` |

---

## 🌟 A regra de ouro

> [!important] Seja consistente
> A regra **mais importante** é a **consistência**: escolha um sistema que funcione para você e **mantenha-o**.

---

## 🔑 Glossário rápido

- **Hostname** — o nome dado a um computador/máquina.
- **RFC 1178** — documento com boas práticas (não obrigatórias) de nomenclatura.
- **Nomenclatura descritiva** — o nome descreve a função (`web-server-prod-01`).
- **Nomenclatura temática** — nomes seguindo um tema (`jupiter`, `mars`).
- **Nomenclatura aleatória** — identificadores únicos sem significado (`vm-1a52`).

---

## ✅ Pontos de revisão

- [ ] Quais são as três recomendações principais do RFC 1178?
- [ ] Por que evitar nomes como "up" ou "down"?
- [ ] Quais caracteres são seguros para usar em um hostname?
- [ ] Cite as três estratégias de nomenclatura e um cenário ideal para cada.
- [ ] Qual é a regra mais importante de todas?

---

## 🔗 Notas relacionadas

- [[DDI Associate - Índice]]
- Aula anterior: [[08 - RRset]]
- Próxima aula: _(a definir conforme você enviar)_
- Relacionado: [[07 - Nomes Legais de DNS e IDN]] (caracteres válidos, case-insensitive)
