---
tipo: conceito
area: Produtos
tags:
- produto
criada: '2024-10-14'
---

"Erro cria Defeito (bug) que por sua vez causa uma Falha. Nem sempre um bug irá resultar em uma falha."

## Conceitos básicos
### Erro
É um resultado incorreto de uma ação humana.

### Defeito ou bug
É uma imperfeição no produto de software

### Falha
É a diferença indesejada entre o que foi observado e o esperado


## Modelo de exemplo

Quando <persona/papel/perfil>
faz <*ação*>
e <*outra ação*>
então <*resultado observado*>
e <*outro resultado observado*>
quando deveria <*resultado esperado*>

Ex (errado): Funcionalidade -> Encontrar Pessoas. Bug -> Filtro por cidade não funciona.

Ex (correto): Funcionalidade -> Encontrar Pessoas. Bug -> Quando o cliente faz um filtro por cidade e seleciona uma cidade específico então a pesquisa retorna pessoas de cidades não selecionadas, quando deveria retornar apenas pessoas das cidades selecionadas no filtro.

Recomendações

1. Utilize o modelo para descrever o bug
2. Associe o bug a funcionalidade;
3. Nunca esqueça dos passos para reprodução do bug.

## Elementos para descrever um bug
### 2 - Descrição

### 3 - Ambiente

### 4 - Passo a passo para reprodução

### 5 - Resultado observado

### 6 - Resultado esperado

### 7 - Evidência

### 8 - Severidade

### 9 - Prioridade

### 10 - Funcionalidade


## Exemplo completo de Bug Report

### 1. **Identificador**

- **Funcionalidade**: Configurações de Usuário
- **Bug**: Quando o usuário acessa as configurações e tenta alterar as informações de perfil e clica no botão "Salvar", o sistema não responde e nenhuma mensagem de erro é exibida, quando deveria salvar as alterações e exibir uma confirmação de sucesso.

### 2. **Descrição**

- O botão "Salvar" na tela de configurações do usuário não está funcionando como esperado. Quando o usuário tenta salvar novas informações de perfil, o sistema não realiza nenhuma ação e as mudanças não são aplicadas.

### 3. **Ambiente**

- **Sistema Operacional**: Windows 10
- **Navegador**: Google Chrome v92
- **Versão do Software**: 1.4.3

### 4. **Passo a passo para reprodução**

1. Fazer login na aplicação com um usuário válido.
2. Navegar até a seção "Configurações de Usuário".
3. Alterar qualquer campo do perfil, como nome ou endereço de e-mail.
4. Clicar no botão "Salvar".
5. Observar que o botão não responde e nenhuma ação é executada.

### 5. **Resultado observado**

- O botão "Salvar" não realiza nenhuma ação após ser clicado e nenhuma mensagem de erro ou feedback é exibida ao usuário.

### 6. **Resultado esperado**

- As alterações no perfil do usuário deveriam ser salvas corretamente e uma mensagem de confirmação deveria ser exibida para o usuário indicando que as mudanças foram aplicadas com sucesso.

### 7. **Evidência**

- [Vídeo anexo] mostrando a tentativa de alterar e salvar os dados sem sucesso.

### 8. **Severidade**

- Alta: Esse bug impede os usuários de atualizar suas informações de perfil, afetando uma funcionalidade essencial do sistema.

### 9. **Prioridade**

- P1: Este bug deve ser corrigido antes do próximo lançamento, pois afeta a experiência central do usuário e pode gerar frustração.

### 10. **Funcionalidade**

- Configurações de Usuário
