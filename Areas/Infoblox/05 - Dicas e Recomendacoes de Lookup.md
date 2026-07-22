---
tipo: aula
area: Infoblox
tags:
- redes/ddi
- redes/dns
- ferramentas
- troubleshooting
- dig
criada: '2026-05-28'
curso: DDI Associate
aula: 5
titulo: Dicas e Recomendações de Lookup
fonte: Infoblox Education
duracao: 2m
dificuldade: Intermediate
---

# Aula 5 — Dicas e Recomendações de Lookup

> [!info] Resumo
> A ferramenta recomendada para trabalhar com DNS é o **`dig`**. Ele segue **todos os padrões**, é **explícito** (faz exatamente o que você manda) e **não usa o cache do cliente** — qualidades que o tornam ideal para troubleshooting. Um detalhe técnico crucial: o `dig` **exige o FQDN com ponto final (trailing dot)** e **não adiciona sufixos**.

---

## 🥇 Por que usar o `dig`

O `dig` é a recomendação para DNS porque:

- **Segue todos os padrões DNS.**
- **Suporta todas as opções**, inclusive avançadas como **DNSSEC**.
- Pode realizar uma **transferência de zona completa (full zone transfer)**.
- **Não lê do cache do cliente** → grande vantagem no troubleshooting (você vê a resposta real, não uma cacheada).

> [!tip] Implementação de referência
> Assim como o **BIND**, o `dig` foi projetado como **implementação de referência**: segue de perto os padrões publicados e **não tem comportamentos proprietários ou fora do padrão**.

---

## 🎯 Explícito e literal

> [!important] O `dig` não tenta te "ajudar"
> Ele **faz exatamente o que você mandar** — nada de adivinhações. Essa literalidade é justamente o que o torna **ótimo para diagnóstico**.

- O `dig` tem **muitas opções**.
- Além das opções de consulta de **cliente**, ele também consegue enviar **todas as opções de DNS que um name server enviaria**.
- Isso é muito útil quando você está **diagnosticando um problema no próprio servidor**.

---

## ⚫ O ponto final (trailing dot) e o FQDN

- Um **FQDN** deveria incluir um **ponto final (trailing dot)**, que representa o **domínio raiz (root)** do DNS.
- O `dig` **não acrescenta sufixos** e **sempre exige que você forneça o FQDN**.
  - Ex.: você deve pedir o lookup de **`example.com.`** (com ponto final), e não apenas `example` ou `example.com`.

> [!note]
> A maioria dos softwares **ignora ou adiciona** o ponto final automaticamente. Mas, no **troubleshooting**, esse ponto é **importante**.

> [!warning] O perigo de omitir o ponto final
> Muitos sistemas **anexam search domains / sufixos** ao final do nome quando não há o ponto.
> Resultado: um lookup de `example.com` pode acabar virando uma busca por **`example.com.local`** — causando **atrasos e problemas** no diagnóstico.

> [!tip] O que o trailing dot significa
> **"Não adicione nada depois deste nome. Faça o lookup exatamente como eu digitei."**

---

## 🧩 Resumo prático

| Característica do `dig` | Benefício no troubleshooting |
|--------------------------|------------------------------|
| Segue todos os padrões (DNSSEC, zone transfer) | Comportamento confiável e completo |
| Não lê do cache do cliente | Mostra a resposta **real**, não a cacheada |
| Explícito / literal | Sem "ajudas" que mascaram problemas |
| Envia opções de cliente **e** de servidor | Diagnostica problemas no próprio servidor |
| Exige FQDN com **ponto final** | Evita anexar sufixos indevidos (ex.: `.local`) |

---

## 🔑 Glossário rápido

- **`dig`** — ferramenta de DNS de referência; explícita, padrão e sem cache de cliente.
- **DNSSEC** — extensão de segurança do DNS (suportada pelo `dig`).
- **Full zone transfer** — cópia completa dos registros de uma zona.
- **FQDN** — nome de domínio completo; idealmente com **ponto final**.
- **Trailing dot (ponto final)** — representa o **root** e diz "não anexe nada".
- **Search domain / sufixo** — domínio anexado automaticamente a nomes curtos (ex.: `.local`).

---

## ✅ Pontos de revisão

- [ ] Cite ao menos três motivos para preferir o `dig` no troubleshooting.
- [ ] Por que "não ler do cache do cliente" é uma vantagem?
- [ ] O que significa o `dig` ser uma "implementação de referência"?
- [ ] O que o **ponto final (trailing dot)** representa e o que ele instrui?
- [ ] Que problema pode surgir ao omitir o ponto final em um lookup?

---

## 🔗 Notas relacionadas

- [[DDI Associate]]
- Aula anterior: [[04 - Softwares Cliente de DNS Comuns]]
- Próxima aula: _(a definir conforme você enviar)_
