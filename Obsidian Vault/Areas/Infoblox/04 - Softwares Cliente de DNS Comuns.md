---
curso: DDI Associate
aula: 4
titulo: Softwares Cliente de DNS Comuns
fonte: Infoblox Education
duracao: 3m
dificuldade: Intermediate
tags:
  - DDI
  - DNS
  - networking
  - ferramentas
  - troubleshooting
data: 2026-05-28
---

# Aula 4 — Softwares Cliente de DNS Comuns

> [!info] Resumo
> Existem várias ferramentas cliente de DNS, e cada uma tem um propósito. Algumas emulam o comportamento de outras aplicações, outras servem para troubleshooting, e outras emulam um resolver recursivo. A regra de ouro: **`dig` é a mais completa e aderente aos padrões**; já `nslookup` e `ping` são populares, mas **traiçoeiros para diagnóstico** se você não souber lê-los.

---

## 🎯 Para que serve um software cliente de DNS

Um software cliente de DNS pode:

- **Emular o comportamento** de outra aplicação;
- **Fazer troubleshooting** (diagnóstico);
- **Emular um resolver recursivo** de DNS.

---

## 🛠️ As ferramentas

### 🥇 `dig`
- A ferramenta **mais rica em recursos** e **mais aderente aos padrões**.
- Desenvolvida e mantida pela **ISC** — o mesmo grupo que faz o **BIND**.
- É a **referência** para análise e troubleshooting de DNS.

### `host`
- Utilitário de **lookup simples**, geralmente já incluso em sistemas **Linux/UNIX**.
- Não é tão completo quanto o `dig`, mas **segue bem os padrões DNS**.
- Uma **alternativa sensata** ao `dig`.

### ⚠️ `nslookup`
- Vem **por padrão em muitos sistemas Windows**.
- Sua intenção **original** era ser uma ferramenta de **emulação de comportamento de cliente** — **não** de troubleshooting.
- Tem características que o tornam **uma má escolha para diagnóstico**.

> [!warning] Cuidado com falsos positivos
> O `nslookup` pode mostrar **falsos positivos** se você não souber **interpretar a saída** ou **ajustar as configurações**. Ele **não foi feito** para troubleshooting.

### ⚠️ `ping`
- **Nunca** foi feito para ser uma ferramenta de troubleshooting de DNS — mas muita gente o usa assim.
- Conveniente por estar **pré-instalado** na maioria dos sistemas.
- **Cada versão do `ping` pode funcionar de forma um pouco diferente.**

> [!warning] Armadilha clássica
> Algumas versões fazem **lookups adicionais silenciosos** (como o `nslookup`) e retornam uma **resposta enganosa**.
> Se um FQDN **não responde ao `ping`**, isso **não significa** que o DNS está com problema. Muitas vezes o **DNS funciona normalmente**, mas há um **problema de rede** impedindo o `ping` de alcançar o destino.

---

## 🌍 Outras formas de testar resolução de nomes

### Navegador web
- Como a maioria dos domínios aponta para uma página web, o **navegador** também serve como cliente DNS.
- Se o **site carrega**, o **DNS daquele site está funcionando**.

### Ferramentas web de DNS lookup
- Existem **vários sites** que fazem DNS lookup online.
- (Veja as **notas suplementares** do curso para uma lista desses sites.)

### 📱 Smartphone
- Você provavelmente já tem um **analisador de DNS no bolso**.
- Útil para **verificar se um registro DNS é visível de fora da sua rede**: o celular consulta a partir da **rede da operadora móvel**, oferecendo uma **perspectiva externa**.
- App recomendado: **ISC Dig** — equivalente mobile do comando `dig` do desktop.

---

## 🧩 Tabela comparativa

| Ferramenta | Plataforma típica | Aderência aos padrões | Bom p/ troubleshooting? | Observação |
|------------|-------------------|------------------------|--------------------------|------------|
| **`dig`** | Linux/UNIX (ISC) | ✅ Alta | ✅ Sim | Mais completa e recomendada |
| **`host`** | Linux/UNIX | ✅ Boa | ✅ Sim (simples) | Alternativa sensata ao `dig` |
| **`nslookup`** | Windows (padrão) | ⚠️ Limitada | ❌ Não | Risco de falsos positivos |
| **`ping`** | Quase todos | ❌ Não é tool de DNS | ❌ Não | Lookups silenciosos enganosos |
| **Navegador** | Todos | — | 🔸 Teste básico | "Carregou = DNS ok" |
| **ISC Dig (mobile)** | Smartphone | ✅ Alta | ✅ Sim | Perspectiva externa via operadora |

---

## 🔑 Glossário rápido

- **`dig`** — ferramenta DNS mais completa e padrão; mantida pela ISC.
- **ISC** — Internet Systems Consortium; mantém o `dig` e o **BIND**.
- **`host`** — utilitário de lookup simples e padrão (Linux/UNIX).
- **`nslookup`** — ferramenta de emulação (Windows); ruim para diagnóstico.
- **`ping`** — teste de conectividade; **não** é ferramenta de DNS.
- **Falso positivo** — resultado enganoso por má leitura/configuração da ferramenta.
- **ISC Dig (mobile)** — versão do `dig` para smartphone; útil para visão externa.

---

## ✅ Pontos de revisão

- [ ] Por que o `dig` é considerado a melhor ferramenta de DNS?
- [ ] Qual a relação entre `dig`, `host`, BIND e a ISC?
- [ ] Por que `nslookup` não é recomendado para troubleshooting?
- [ ] Por que um FQDN não responder ao `ping` **não** indica necessariamente um problema de DNS?
- [ ] Como o smartphone fornece uma "perspectiva externa" para validar registros DNS?

---

## 🔗 Notas relacionadas

- [[DDI Associate - Índice]]
- Aula anterior: [[03 - Terminologia e Definicoes do DNS]]
- Próxima aula: _(a definir conforme você enviar)_
