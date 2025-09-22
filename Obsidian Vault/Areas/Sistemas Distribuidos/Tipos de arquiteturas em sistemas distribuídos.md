#### **a) Arquitetura Centralizada (Cliente-Servidor)**

- **Descrição:** Um servidor central detém a maior parte dos dados e da lógica. Os clientes se conectam a ele para solicitar informações ou executar ações.
    
- **Vantagens:** Simplicidade de gerenciamento, controle e segurança centralizados.
    
- **Desvantagens:** Ponto único de falha (se o servidor cair, tudo para), gargalo de desempenho e escalabilidade limitada.
    

#### **b) Arquitetura Descentralizada (Peer-to-Peer - P2P)**

- **Descrição:** Não existe um servidor central. Todos os participantes (pares ou _peers_) são iguais e se comunicam diretamente entre si, compartilhando recursos e dados.
    
- **Vantagens:** Alta resiliência (não há ponto único de falha), escalabilidade natural (a capacidade da rede aumenta com mais participantes) e resistência à censura.
    
- **Desvantagens:** Maior complexidade para garantir a consistência dos dados, descoberta de outros pares e segurança. Exemplos clássicos são o BitTorrent e as criptomoedas.
    

#### **c) Arquitetura Híbrida**

- **Descrição:** Combina elementos dos dois modelos para obter o melhor de ambos os mundos.
    
- **Exemplos:**
    
    - **Spotify/Skype:** Usam servidores centrais para autenticação e gerenciamento de contas (centralizado), mas a transmissão de dados (música/chamada) pode ocorrer de forma mais direta entre os usuários ou através de servidores de borda (descentralizado).
        
    - **Computação em Nuvem com CDN (Content Delivery Network):** A lógica principal da aplicação está em servidores centrais, mas o conteúdo estático (imagens, vídeos) é distribuído em uma rede descentralizada de servidores para estar mais perto do usuário, reduzindo a latência.