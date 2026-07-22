---
tipo: aula
area: Infoblox
tags:
- redes/ddi
- redes/dns
- root-servers
- anycast
- tld
- infraestrutura
criada: '2026-05-28'
curso: DDI Associate
aula: 12
titulo: Root Name Servers e Endereços IP
fonte: Infoblox Education
duracao: 1m
dificuldade: Intermediate
---

# Aula 12 — Root Name Servers e Endereços IP

> [!info] Resumo
> Os **Root Name Servers** são os servidores autoritativos da **zona raiz (root)** do DNS — o **primeiro passo** de toda resolução de nomes. Existem **13 root servers** (operados por **12 entidades**), todos usando **Anycast** para serem replicados por milhares de instâncias pelo mundo. Todo servidor recursivo precisa conhecê-los por IP, lista conhecida como **root hints**.

---

## 🌱 O que são os Root Name Servers

- São os **servidores autoritativos da zona raiz (root)** do DNS — às vezes representada por um **único ponto (`.`)**.
- São uma parte **crítica da infraestrutura da internet**, pois representam o **primeiro passo** na resolução de nomes.
- **Todo servidor recursivo do mundo** precisa conhecê-los **por endereço IP**.

> [!note] Root Hints
> A lista de endereços IP dos root name servers é geralmente chamada de **"root hints"**.

---

## 🔢 Quantidade, operadores e Anycast

- Existem **13 root name servers** no mundo...
- ...operados por **12 entidades diferentes**.
- Eles usam o protocolo **Anycast**, o que permite que cada um seja atendido por **centenas/milhares de instâncias de servidor** espalhadas pelo mundo.

> [!tip] Por que isso importa
> Graças ao **Anycast**, "13 servidores" não significa apenas 13 máquinas: na prática, há **milhares de réplicas** distribuídas globalmente, trazendo **resiliência** e **proximidade** (menor latência).

---

## 🌍 Responsabilidade: todos os TLDs do mundo

Os root servers são responsáveis por **todos os Top-Level Domains (TLDs)**, incluindo:

- **gTLDs (generic TLDs):** `com`, `org`, `net`, `gov`.
- **ccTLDs (country code TLDs):** `BE` (Bélgica), `CA` (Canadá), etc.

---

## 📅 2014 — A explosão de novos TLDs

> [!important] Mudança de regras
> Em **2014**, as regras mudaram, permitindo que **qualquer pessoa** solicitasse **qualquer TLD** além dos tradicionais.

- Isso provocou uma **onda de novos TLDs**: milhares de domínios como `.free`, `.pizza`, `.tokyo` e `.zip`.
- Foi uma mudança significativa que **expandiu o namespace** da internet...
- ...e trouxe **implicações de segurança de longo alcance**.

> [!warning] Implicação de segurança
> A proliferação de novos TLDs (ex.: `.zip`, que coincide com uma extensão de arquivo) ampliou a superfície para **confusão e abusos**, como phishing — por isso a aula destaca as "far-reaching security implications".

---

## 🔑 Glossário rápido

- **Root Name Server** — servidor autoritativo da zona raiz; primeiro passo da resolução.
- **Zona raiz (root) / `.`** — o topo da hierarquia do DNS.
- **Root hints** — lista de IPs dos root servers que todo recursivo precisa conhecer.
- **13 servers / 12 entidades** — número de root servers e de operadores.
- **Anycast** — protocolo que replica cada root server em milhares de instâncias.
- **TLD** — Top-Level Domain; gTLD (genérico) e ccTLD (código de país).
- **Expansão de 2014** — abertura para novos TLDs (`.pizza`, `.tokyo`, `.zip`...).

---

## ✅ Pontos de revisão

- [ ] O que é a zona raiz e por que os root servers são o "primeiro passo" da resolução?
- [ ] O que são os "root hints" e quem precisa deles?
- [ ] Quantos root servers existem e quantas entidades os operam?
- [ ] O que o **Anycast** permite, na prática?
- [ ] Qual a diferença entre gTLD e ccTLD? Dê exemplos.
- [ ] O que mudou em 2014 e por que isso teve implicações de segurança?

---

## 🔗 Notas relacionadas

- [[DDI Associate - Índice]]
- Aula anterior: [[11 - Dados Autoritativos]]
- Próxima aula: _(a definir conforme você enviar)_
- Relacionado: [[01 - Historia do DNS]] (árvore invertida, TLDs/ccTLDs) · [[03 - Terminologia e Definicoes do DNS]] (recursivo vs. autoritativo)
