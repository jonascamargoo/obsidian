---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware
criada: '2024-10-14'
---

Uma máquina virtual (VM) é um ambiente computacional completamente isolado e independente, criado por meio de software de virtualização. Essa tecnologia permite a execução de sistemas operacionais e aplicativos dentro de um ambiente virtualizado, isolado do sistema operacional hospedeiro. As VMs possibilitam a consolidação de recursos, permitindo que várias instâncias de sistemas operacionais coexistam em um único servidor físico. Isso oferece flexibilidade, eficiência e gerenciamento simplificado de recursos computacionais.

### Por que máquinas virtuais?

■ **A crescente importância do isolamento e segurança em sistemas modernos**

	Com o avanço tecnológico, a necessidade de isolamento e segurança tornou-se cada vez mais crucial em sistemas modernos. As Máquinas Virtuais desempenham um papel fundamental nesse contexto, proporcionando ambientes isolados que podem operar de forma independente, protegendo contra ameaças de segurança e garantindo a integridade dos sistemas.

■ **As falhas em segurança e confiabilidade dos sistemas operacionais padrão**

	Os sistemas operacionais padrão frequentemente apresentam vulnerabilidades que podem ser exploradas, comprometendo a segurança e a confiabilidade dos sistemas. O uso de VMs oferece uma camada adicional de segurança, permitindo a execução de ambientes isolados e reduzindo o impacto de potenciais falhas nos sistemas operacionais subjacentes.

■ **O compartilhamento de um único computador entre muitos usuários não relacionados, especialmente para computação em nuvem**

	Em ambientes de computação em nuvem, onde a eficiência e o compartilhamento de recursos são fundamentais, as VMs desempenham um papel crucial. Elas permitem que um único computador seja compartilhado entre vários usuários independentes, garantindo isolamento entre as instâncias e maximizando a utilização dos recursos disponíveis.

■ **Os aumentos dramáticos na velocidade bruta dos processadores ao longo das décadas, o que tornou o overhead das VMs mais aceitável**

	O avanço significativo na velocidade dos processadores ao longo das décadas contribuiu para tornar o overhead das Máquinas Virtuais mais aceitável. Isso possibilitou a execução eficiente de ambientes virtuais, permitindo benefícios como a consolidação de recursos, a migração de máquinas virtuais em tempo real e uma melhor utilização dos avanços tecnológicos sem comprometer significativamente o desempenho do sistema.

-------------------------------------------------------------------------------------------------

- Software que suporta uma máquina virtual chama *virtual machine monitor (VMM)* ou hypervisor
- O hardware que hospeda uma VM é chamado de *host* e seus recursos são compartilhados com as VMs convidadas (guest)


### VMs proporcionam mais dois benefícios comercialmente significativos:

1. **Gerenciamento de Software:** VMs oferecem uma abstração que pode executar a pilha completa de software, incluindo sistemas operacionais antigos como o DOS. Em uma implementação típica, algumas VMs podem executar sistemas operacionais legados, muitas executando a versão estável atual do sistema operacional e algumas testando a próxima versão do sistema operacional. Essa flexibilidade no gerenciamento de ambientes de software é valiosa para diversos fins, como manter a compatibilidade com aplicativos mais antigos e testar novos lançamentos de software.
    
2. **Gerenciamento de Hardware:** VMs contribuem para um gerenciamento eficaz de hardware. Em configurações tradicionais, as aplicações frequentemente são executadas em servidores separados para garantir compatibilidade com versões específicas do sistema operacional, aumentando a confiabilidade. VMs possibilitam que essas pilhas de software independentes sejam executadas no mesmo hardware, consolidando o número de servidores físicos necessários. Além disso, alguns Monitores de Máquina Virtual (VMMs) suportam a migração ao vivo de uma VM em execução para um computador diferente. Essa capacidade pode ser utilizada para equilibrar a carga entre servidores ou para evacuar de hardware com falha, contribuindo para uma melhor utilização de recursos e confiabilidade do sistema.

### **Interface Hardware/Software na Amazon Web Services (AWS)**

A Amazon Web Services (AWS) utiliza máquinas virtuais em seu serviço de computação em nuvem, EC2, por cinco razões fundamentais:

1. **Isolamento para Proteção do Usuário:** O EC2 possibilita à AWS proteger os usuários entre si ao compartilhar o mesmo servidor.
    
2. **Distribuição Simplificada de Software:** A AWS utiliza máquinas virtuais para otimizar a distribuição de software em um computador de escala de armazém. Os clientes instalam uma imagem de máquina virtual previamente configurada com o software necessário, e a AWS a distribui eficientemente para todas as instâncias desejadas.
    
3. **Gerenciamento de Recursos através do Encerramento de VMs:** Os clientes (e a AWS) podem "encerrar" uma máquina virtual de forma confiável para controlar o uso de recursos quando os clientes concluem suas tarefas.
    
4. **Ocultação da Identidade do Hardware:** Máquinas virtuais ocultam a identidade do hardware subjacente, permitindo que a AWS continue utilizando servidores mais antigos e introduza servidores mais recentes e eficientes. Os clientes esperam que o desempenho da instância esteja alinhado com as "Unidades de Computação EC2," uma métrica definida pela AWS para representar a capacidade equivalente de CPU de um processador AMD Opteron de 1,0–1,2 GHz de 2007 ou um processador Intel Xeon de 2007. Embora servidores mais recentes geralmente ofereçam mais Unidades de Computação EC2, a AWS pode continuar alugando servidores mais antigos desde que sejam economicamente viáveis.
    
5. **Alocação Flexível de Recursos:** Monitores de Máquina Virtual (VMMs) fornecem controle sobre o uso de processador, rede e espaço em disco, permitindo que a AWS ofereça diversos tipos de instâncias com diferentes pontos de preço nos mesmos servidores subjacentes. Em 2020, a AWS apresentou mais de 200 tipos de instâncias, variando de menos de meio centavo por hora (por exemplo, t3a.nano a $0,0047) a mais de $25 (por exemplo, x1e.32xlarge otimizado para memória a $26,69), demonstrando uma faixa de preço superior a 5000:1.

### Custo da virtualização

No geral, o custo da virtualização de processador depende da carga de trabalho. Programas de usuário intensivos em processamento, ou seja, aqueles que consomem significativamente os recursos do processador, geralmente não apresentam overhead de virtualização, pois o sistema operacional (SO) é raramente invocado, permitindo que tudo funcione em velocidades nativas. Por outro lado, cargas de trabalho intensivas em entrada/saída (I/O) geralmente também são intensivas em operações do sistema operacional, executando muitas chamadas de sistema e instruções privilegiadas que podem resultar em um alto overhead de virtualização.

Entretanto, se a carga de trabalho intensiva em I/O também for limitada pelo I/O, o custo da virtualização do processador pode ser totalmente oculto, uma vez que o processador muitas vezes fica ocioso aguardando operações de I/O. Em resumo, quando a carga de trabalho é I/O-bound (limitada pelo I/O), o impacto da virtualização no desempenho do processador pode ser minimizado, uma vez que o processador pode ser efetivamente utilizado durante os períodos em que está aguardando operações de I/O. Ou seja, é impossível saber o trad-off, pois poderia estar sendo usado para várias outras coisas (o preço da ociosidade é incalculável).

O overhead de virtualização é determinado tanto pelo número de instruções que precisam ser emuladas pelo Monitor de Máquina Virtual (VMM) quanto pelo tempo que cada uma dessas instruções leva para ser emulada. Portanto, quando as máquinas virtuais (VMs) convidadas executam o mesmo conjunto de instruções de conjunto de arquitetura (ISA, do inglês Instruction Set Architecture) que o hospedeiro, como é assumido aqui, a arquitetura e o VMM têm como objetivo executar quase todas as instruções diretamente no hardware nativo, minimizando assim o impacto do overhead de virtualização.


### Requirements of a Virtual Machine Monitor, what they do?


Basicamente, funcionar como uma interface do guest software, protegendo os estados de um guest para o outro. "Guest software should behave on a VM exactly as if it were running on the native hardware, except for performance-related behavior or limitations of fixed resources shared by multiple VMs. Guest software should not be able to change allocation of real system resources directly.
