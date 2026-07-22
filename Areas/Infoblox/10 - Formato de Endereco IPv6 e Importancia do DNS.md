---
curso: DDI Associate
aula: 10
titulo: Formato de Endereço IPv6 e a Importância Crescente do DNS
fonte: Infoblox Education
dificuldade: Intermediate
tags:
  - DDI
  - DNS
  - IPv6
  - enderecamento
  - RFC8200
data: 2026-05-28
---

# Aula 10 — Formato de Endereço IPv6 e a Importância Crescente do DNS

> [!info] Resumo
> Endereços **IPv6** são escritos em **hexadecimal**, em blocos de quatro dígitos separados por dois-pontos — longos demais para qualquer humano memorizar. Justamente por isso, à medida que a internet migra de IPv4 para IPv6, o **DNS se torna ainda mais crítico**.

---

## 🔢 Formato de endereço IPv6

- **IPv4** usa um formato **decimal** simples → ex.: `192.168.1.1`.
- **IPv6** é longo demais para isso, então usa **hexadecimal**, agrupado em **blocos de 4 dígitos** separados por **dois-pontos (`:`)**.

**Endereço IPv6 completo:**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

### ✂️ Abreviação

Como os endereços IPv6 podem ser bem longos, há formas de **encurtá-los**:

- Grupos **consecutivos de zeros** podem ser representados por um **duplo dois-pontos (`::`)**.
- Exemplo comum:
```
fe80::ac7b:35ff:fe44:6c0c
```

> [!note]
> O `::` substitui uma sequência de grupos de zeros — e só pode aparecer **uma vez** em um endereço (regra geral do IPv6).

| | IPv4 | IPv6 |
|---|------|------|
| **Base numérica** | Decimal | Hexadecimal |
| **Separador** | Ponto (`.`) | Dois-pontos (`:`) |
| **Exemplo** | `192.168.1.1` | `2001:0db8:85a3:0000:0000:8a2e:0370:7334` |
| **Abreviação** | — | `::` para grupos de zeros |

---

## 📈 A importância crescente do DNS

- A internet está migrando, lenta mas seguramente, de **IPv4 para IPv6**.
- Conforme essa transição acontece, o **DNS se torna ainda mais crítico**.

> [!tip] Reflexão da aula
> Se você já tem dificuldade de lembrar os endereços **IPv4** dos seus dispositivos, imagine tentar lembrar os endereços **IPv6** deles — fica fácil entender por que o **DNS é essencial em uma rede IPv6**.

---

## 📜 Referências (RFCs)

- IPv6 foi originalmente especificado no **RFC 2460**.
- Posteriormente atualizado pelo **RFC 8200**.

---

## 🔑 Glossário rápido

- **IPv6** — protocolo de endereçamento em hexadecimal, blocos de 4 dígitos separados por `:`.
- **Hexadecimal** — base numérica usada no IPv6 (0–9, a–f).
- **`::` (duplo dois-pontos)** — abrevia grupos consecutivos de zeros (uma vez por endereço).
- **RFC 2460** — especificação original do IPv6.
- **RFC 8200** — atualização da especificação do IPv6.

---

## ✅ Pontos de revisão

- [ ] Qual a diferença de formato entre IPv4 e IPv6 (base e separador)?
- [ ] Como se abrevia uma sequência de grupos de zeros em um endereço IPv6?
- [ ] Por que o DNS se torna **ainda mais importante** com o IPv6?
- [ ] Em quais RFCs o IPv6 foi especificado e atualizado?

---

## 🔗 Notas relacionadas

- [[DDI Associate - Índice]]
- Aula anterior: [[09 - Dicas para Nomear seus Computadores]]
- Próxima aula: _(a definir conforme você enviar)_
- Relacionado: [[02 - Importancia do DNS]] (por que nomes > IPs) · [[03 - Terminologia e Definicoes do DNS]] (registro AAAA = IPv6)
