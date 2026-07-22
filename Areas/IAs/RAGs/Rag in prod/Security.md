---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/llmops
criada: '2026-02-24'
---

**Data:** 24/02/2026

**Tópico:** #Cybersecurity #RAG #DataPrivacy #InfoSec #VectorDatabase

---

## 🔒 1. Controle de Acesso e Vazamento via Prompt

A primeira vulnerabilidade a ser considerada é a extração de dados pelo próprio usuário. Um prompt bem elaborado pode convencer o LLM a citar diretamente informações confidenciais recuperadas da sua base de conhecimento.

### Estratégias de Mitigação na Aplicação:

- **Autenticação Direcionada:** A solução mais direta é autenticar os usuários de forma apropriada à informação que eles têm permissão para acessar (ex: garantir que apenas funcionários logados façam requisições).
    
- **Multi-tenancy e RBAC:** Os dados devem ser divididos em múltiplos "inquilinos" (tenants) com base em privilégios de controle de acesso baseado em funções (RBAC). Na prática, se o prompt leva a uma busca no banco vetorial, o usuário só deve ter acesso a documentos permitidos pelo seu nível hierárquico.
    

> [!CAUTION] **Filtros de Metadados vs. Segurança Real** Manter todos os documentos em um único _tenant_ e usar filtros de metadados para determinar o acesso é uma técnica muito propensa a falhas. A filtragem de metadados é excelente para personalização, mas não para segurança. A abordagem confiável é ter múltiplos _tenants_ armazenados separadamente.

---

## ☁️ 2. Risco de Exfiltração via Provedores de LLM

O envio de prompts para um provedor externo de LLM para gerar respostas cria uma brecha significativa. O prompt "aumentado" conterá pedaços de texto (chunks) recuperados da sua base privada, fazendo com que você perca o controle sobre a segurança desses dados nesse momento.![[Pasted image 20260224002659.png]]
- **Solução On-premises (Local):** Se o risco não for tolerável, você pode optar por rodar o sistema RAG inteiramente em hardware local (on-premises).
    
- **Trade-off de Engenharia:** Isso exige hospedar tanto o banco de dados vetorial quanto o LLM em infraestrutura própria, introduzindo complexidade adicional e custos de _overhead_. No entanto, garante o controle total do conteúdo em todo o pipeline.
    

---

## 🔐 3. Criptografia no Banco Vetorial e o Algoritmo ANN

Assim como qualquer banco de dados tradicional, a base de conhecimento pode sofrer ataques diretos. Em bancos tradicionais, o conteúdo é protegido com criptografia para impedir o acesso de hackers. Porém, os bancos vetoriais possuem uma restrição arquitetural:

- **O Problema do ANN:** Para que algoritmos de busca de vizinhos mais próximos (ANN - _Approximate Nearest Neighbor_) funcionem, as representações vetoriais densas dos documentos precisam ser mantidas **descriptografadas na memória**.
    
- **Separação Texto/Vetor:** O texto bruto dos _chunks_ pode ser armazenado criptografado, sendo descriptografado apenas no momento de construir o prompt. Isso adiciona uma camada de segurança extra, mas introduz complexidade e possível latência ao sistema.
    

---

## 🧬 4. O Vetor de Ataque de Reconstrução Semântica

Mesmo que você criptografe o texto bruto, manter os vetores densos não criptografados na memória apresenta um risco cibernético avançado.

- **Reconstrução de Texto:** Pesquisas recentes demonstram que é possível reconstruir o texto original a partir de suas representações vetoriais densas. Ou seja, um hacker com acesso ao banco poderia usar técnicas experimentais para extrair informações confidenciais a partir dos _embeddings_.
    

### Técnicas Experimentais de Mitigação:

Para combater a reconstrução, pesquisadores estão explorando métodos como:

1. Adição de ruído aos vetores densos.
    
2. Aplicação de transformações matemáticas.
    
3. Redução de dimensionalidade que preserve distâncias, mas obscureça o significado semântico.
    

> [!WARNING] **Trade-off Operacional** Cada uma dessas técnicas de ofuscação aumenta a complexidade do _retriever_ e tende a reduzir a performance geral do sistema.