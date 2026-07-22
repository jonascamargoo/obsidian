---
tipo: conceito
area: IAs
tags:
- ia
criada: '2025-03-17'
---

## O que é?

É um protocolo open-source que padroniza o fornecimento de contexto para as LLMs. Promove a flexibilidade entre a troca de provedores LLMs, mantem os dados seguros dentro da nossa infraestrutura. Além disso, fornece uma lista crescente de integrações pré-configuradas que sua LLM pode conectar diretamente.

## General Architecture

Segue uma arquitetura client-server, onde a aplicação pode conectar com vários servidores.
![[Pasted image 20250317170634.png]]


- **Hosts MCP**: Programas como Claude Desktop, IDEs ou ferramentas de IA que desejam acessar dados por meio do MCP.

- **Clientes MCP**: Clientes do protocolo que mantêm conexões 1:1 com servidores.

- **Servidores MCP**: Programas leves que expõem funcionalidades específicas por meio do **Model Context Protocol** padronizado.

- **Fontes de Dados Locais**: Arquivos, bancos de dados e serviços do seu computador que os servidores MCP podem acessar com segurança.

- **Serviços Remotos**: Sistemas externos disponíveis na internet (por exemplo, via APIs) aos quais os servidores MCP podem se conectar.
