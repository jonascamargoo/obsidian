---
curso: DDI Associate
aula: 7
titulo: Nomes Legais de DNS e IDN
fonte: Infoblox Education
duracao: 2m
dificuldade: Intermediate
tags:
  - DDI
  - DNS
  - nomes
  - IDN
  - punycode
  - RFC1123
data: 2026-05-28
---

# Aula 7 — Nomes Legais de DNS e IDN

> [!info] Resumo
> Nomes DNS têm **limites de tamanho** (255 caracteres no total, 127 labels, 63 caracteres por label) e, na prática, um **conjunto restrito de caracteres** (A–Z, 0–9 e hífen), conforme o **RFC 1123**. Para suportar outros idiomas, surgiram os **IDN (Internationalized Domain Names)**, codificados em **Punycode** — sempre começando com `xn--`.

---

## 📏 Limites de tamanho de um nome DNS

| Elemento | Limite |
|----------|--------|
| **Nome completo** | máx. **255** caracteres |
| **Número de labels** | máx. **127** labels |
| **Cada label** | máx. **63** caracteres |

> [!note] O que é uma "label"
> Uma **label** é a seção do nome **entre os pontos**.
> Em `www.example.com`: `www` é uma label, `example` é uma label e `com` é uma label.

---

## 🔤 Caracteres permitidos

- **Tecnicamente**, a especificação do DNS aceita **qualquer caractere**.
- **Na prática**, as implementações de software seguem as restrições do **RFC 1123** para hostnames da internet, permitindo apenas:
  - **Letras** A–Z
  - **Dígitos** 0–9
  - **Hífen / traço** ( - )

> [!important] Detalhes importantes
> - O DNS é **case-insensitive**: maiúsculas e minúsculas são tratadas como iguais.
> - O **underscore (`_`) NÃO pode** ser usado em um **hostname**.
> - **Exceção:** há casos especiais em que o underscore é permitido, como em um **registro SRV**.

---

## 🌍 IDN — Internationalized Domain Names

- Originalmente, o DNS só permitia registrar nomes com **caracteres ingleses**.
- A especificação evoluiu para permitir nomes em **outros idiomas** (grego, coreano, etc.).
- Esses nomes são chamados de **IDN (Internationalized Domain Names)**.
- Para viabilizá-los, foi criado um esquema de codificação chamado **Punycode**.
- Existem **conversores de software** que traduzem entre **Unicode** ↔ **Punycode**.

> [!tip] Como reconhecer um IDN
> Todos os nomes IDN no DNS **começam com `xn--`**.
> Ao encontrar um nome iniciado por esses quatro caracteres, use um **conversor IDN** para transformá-lo de volta em Unicode e revelar a representação correta no idioma original.

**Exemplos da aula (domínios fictícios):**

| Idioma / palavra | Exibição (Unicode) | Interno no DNS (Punycode) |
|------------------|--------------------|---------------------------|
| Coreano — "comida" | escrita coreana | `xn--...` |
| Grego — "amor" | escrita grega | `xn--...` |

> [!note]
> À esquerda vê-se como o nome **aparece** na escrita do idioma; à direita, como ele é **representado internamente** no DNS via Punycode.

---

## 🔑 Glossário rápido

- **Label** — seção do nome entre pontos (máx. 63 caracteres).
- **Limite de nome** — 255 caracteres / 127 labels.
- **RFC 1123** — define os caracteres válidos para hostnames (A–Z, 0–9, hífen).
- **Case-insensitive** — maiúsculas/minúsculas tratadas igualmente.
- **Underscore (`_`)** — proibido em hostname, salvo casos especiais (ex.: SRV).
- **IDN** — Internationalized Domain Name; nomes em outros idiomas.
- **Punycode** — codificação que representa Unicode em caracteres DNS válidos.
- **`xn--`** — prefixo que identifica um nome IDN no DNS.

---

## ✅ Pontos de revisão

- [ ] Quais são os três limites de tamanho de um nome DNS?
- [ ] O que é uma "label"? Identifique as labels em `www.example.com`.
- [ ] Quais caracteres são permitidos segundo o RFC 1123?
- [ ] O DNS diferencia maiúsculas de minúsculas? E quanto ao underscore?
- [ ] O que é um IDN e qual codificação o viabiliza?
- [ ] Como reconhecer um nome IDN olhando para ele?

---

## 🔗 Notas relacionadas

- [[DDI Associate - Índice]]
- Aula anterior: [[06 - Anatomia de uma Mensagem DNS]]
- Próxima aula: _(a definir conforme você enviar)_
