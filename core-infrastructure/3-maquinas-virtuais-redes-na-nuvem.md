
# Máquinas virtuais e redes na nuvem

## Redes de nuvem privada virtual


Muitos usuários começam com o Google Cloud definindo a própria nuvem privada virtual dentro do primeiro projeto ou começando com a nuvem privada virtual padrão. Mas o que é uma nuvem privada virtual?
 
Nuvem privada virtual, ou VPC, é um modelo de computação em nuvem seguro, individual e privado hospedado em uma nuvem pública como o Google Cloud.
 
Em uma VPC, os clientes podem executar códigos, armazenar dados, hospedar sites e fazer tudo que poderiam fazer em uma nuvem privada comum. Mas essa nuvem privada é hospedada remotamente por um provedor de nuvem pública.
 
Isso significa que a VPC combina a escalonabilidade e a praticidade da computação em nuvem pública com o isolamento de dados da computação em nuvem privada.
 
As redes VPC conectam recursos do Google Cloud entre si e à Internet. Isso inclui segmentar redes, usar regras de firewall para restringir o acesso a instâncias e criar rotas estáticas para encaminhar tráfego para destinos específicos. Uma coisa que costuma surpreender muitos usuários novos do Google Cloud. As redes VPC do Google são globais.


Elas também podem ter sub-redes, que são segmentos da grande rede em qualquer região do Google Cloud no mundo inteiro. As sub-redes podem abranger as zonas que compõem uma região. Essa arquitetura facilita a definição de layouts de rede com escopo global.

Os recursos podem até estar em zonas diferentes na mesma sub-rede.

A sub-rede pode ser aumentada expandindo o intervalo de endereços IP alocados a ela, e isso não afetará as máquinas virtuais que já estão configuradas.

Por exemplo, vamos pegar uma VPC com uma rede que atualmente tem uma sub-rede definida na região us-east1 do Google Cloud. Se a VPC tiver duas VMs do Compute Engine anexadas a ela, elas são vizinhas na mesma sub-rede, mesmo que estejam em zonas diferentes.
1 
Esse recurso pode ser usado para criar soluções que são resilientes a interrupções, mas que mantêm um layout de rede simples.

## Compute Engine

Mais cedo no curso, vimos a infraestrutura como serviço, ou IaaS. Agora vamos explorar a solução IaaS do Google Cloud: o Compute Engine.

Com o Compute Engine, os usuários podem criar e executar máquinas virtuais na infraestrutura do Google. Não há investimentos iniciais e milhares de CPUs virtuais podem ser executadas em um sistema projetado para ser rápido e oferecer desempenho consistente. Cada máquina virtual contém o poder e a funcionalidade de um sistema operacional completo. Isso significa que a máquina virtual pode ser configurada como um servidor físico, com a especificação da quantidade necessária de CPU e memória, quantidade e tipo de armazenamento necessários e sistema operacional.

Uma instância de VM pode ser criada no Console do Google Cloud, uma ferramenta baseada na Web para gerenciar projetos e recursos do Google Cloud, ou na ferramenta de linha de comando gcloud. A instância pode executar imagens do Linux e do Windows Server fornecidas pelo Google ou qualquer versão personalizada dessas imagens. Também é possível criar e executar imagens de outros sistemas operacionais e reconfigurar máquinas virtuais com flexibilidade.

Uma maneira rápida de começar a usar o Google Cloud é pelo Cloud Marketplace, que oferece soluções do Google e de fornecedores terceirizados. Com essas soluções, não há necessidade de configurar manualmente o software, instâncias de VM, configurações de rede ou armazenamento, mas muitas podem ser modificadas antes do lançamento, se necessário.

A maioria dos pacotes de software no Cloud Marketplace está ali sem custo extra além das taxas normais de uso dos recursos do Google Cloud. Algumas imagens do Cloud Marketplace cobram taxas de uso, principalmente as publicadas por terceiros com software licenciado comercialmente. Mas todas mostram estimativas das cobranças mensais antes de serem lançadas.

Você deve querer saber estrutura de preços e faturamento do Compute Engine.

Para o uso de máquinas virtuais, o Compute Engine cobra por segundo com mínimo de um minuto. E os descontos por uso prolongado são aplicados automaticamente enquanto as VMs são executadas. Portanto, para cada VM executada por mais de 25% de um mês, o Compute Engine aplica automaticamente um desconto para cada minuto adicional. O Compute Engine também oferece desconto por compromisso de uso. Para cargas de trabalho estáveis ​​e previsíveis, uma quantidade específica de vCPUs e memória pode ser comprada com um desconto de até 57% em relação aos preços normais em troca do compromisso com um período de uso de um ou três anos. E depois temos as VMs preemptivas. Se você tiver uma carga de trabalho que não exige que um humano espere que ela termine, como um job em lote que analisa um grande conjunto de dados. É possível economizar até 90% ao escolher VMs preemptivas para executar o job.

A VM preemptiva é diferente de uma VM comum do Compute Engine em apenas um aspecto. O Compute Engine tem permissão para encerrar um job se os recursos dele são necessários em outro lugar. É possível economizar com VMs preemptivas, é preciso garantir que o job pode ser interrompido e reiniciado. Em termos de armazenamento, o Compute Engine não exige uma opção ou tipo de máquina específicos para obter alta capacidade entre processamento e discos permanentes. Esse é o padrão e não tem nenhum custo extra para você. E, por fim, você paga apenas pelo que precisar com tipos de máquina personalizados.

O Compute Engine permite escolher as propriedades de máquina das instâncias, como o número de CPUs virtuais e a quantidade de memória, com o uso de um conjunto de tipos de máquina predefinidos ou com a criação de seus próprios tipos personalizados.

- **Escalonamento de máquinas virtuais:**

Como acabamos de ver, com o Compute Engine, é possível escolher as propriedades de máquina mais apropriadas para instâncias, como o número de CPUs virtuais e a quantidade de memória, usando tipos de máquina predefinidos ou criando tipos de máquina personalizados.

Para isso, o Compute Engine tem um recurso chamado escalonamento automático, em que as VMs podem ser adicionadas ou subtraídas de um aplicativo com base nas métricas de carga. A outra parte de fazer esse trabalho é equilibrar o tráfego de entrada entre as VMs. A nuvem privada virtual do Google, VPC, aceita vários tipos diferentes de balanceamento de carga, que vamos explorar em breve. Com o Compute Engine, é possível configurar VMs muito grandes, que são ótimas para cargas de trabalho como bancos de dados na memória e análises com uso intensivo de CPU. Mas a maioria dos clientes começa com o escalonamento horizontal, não vertical.

O número máximo de CPUs por VM está vinculado à família de máquinas e também é limitado pela cota disponível para o usuário, que depende da zona.

## Compatibilidades importantes com VPC

Agora vamos explorar alguns dos recursos de compatibilidade mais importantes da nuvem privada virtual.


Assim como redes físicas, as VPCs têm tabelas de roteamento. As tabelas de roteamento das VPCs são integradas e você não precisa provisionar ou gerenciar o roteador. Elas encaminham o tráfego de uma instância a outra dentro da mesma rede, entre sub-redes, ou mesmo entre zonas do Google Cloud, sem exigir um endereço IP externo.

Também não é preciso provisionar ou gerenciar firewalls para o Google Cloud. As VPCs fornecem um firewall distribuído global que pode restringir o acesso a instâncias por meio do tráfego de entrada e de saída. As regras de firewall podem ser definidas por tags de metadados em instâncias do Compute Engine, o que é muito prático.

Por exemplo, é possível marcar todos os servidores da Web com, digamos, "Web" e escrever uma regra de firewall dizendo que o tráfego nas portas 80 ou 443 é permitido em todas as VMs com a tag "Web", não importa qual seja o endereço IP.

Você lembra que as VPCs pertencem a projetos do Google Cloud, mas e se sua empresa tiver vários projetos do Google Cloud e as VPCs precisarem conversar entre si?

Com o peering de VPCs, uma relação entre duas VPCs pode ser estabelecida para trocar tráfego. Como alternativa, para usar todo o poder do Identity Access Management, IAM, para controlar quem e o que em um projeto pode interagir com uma VPC em outro, é possível configurar uma VPC compartilhada.

## Cloud Load Balancing

Já vimos que as máquinas virtuais podem ser escalonadas automaticamente para responder a cargas variáveis. Mas como seus clientes chegam ao seu aplicativo quando ele pode ser provisionado por quatro VMs em um momento e por 40 VMs em outro?

Isso é feito com o Cloud Load Balancing. Um balanceador de carga distribui o tráfego de usuários em várias instâncias de um aplicativo. Ao distribuir a carga, o balanceamento de carga reduz o risco de problemas de desempenho nos aplicativos.

O Cloud Load Balancing é um serviço totalmente distribuído, definido por software e gerenciado para todo o seu tráfego. E como você não gerencia as VMs onde os balanceadores de carga são executados não precisa escaloná-los ou gerenciá-los. É possível colocar o Cloud Load Balancing na frente de todo o seu tráfego: HTTP ou HTTPS, outros tráfegos TCP e SSL e também tráfego UDP. O Cloud Load Balancing oferece balanceamento de carga entre regiões, incluindo failover multirregional automático, que redireciona o tráfego em frações caso os back-ends percam a integridade. O Cloud Load Balancing reage rapidamente a mudanças em usuários, tráfego, rede, integridade do back-end e outras condições relacionadas. E se você antecipar um grande aumento na demanda? Digamos que seu jogo on-line já seja um sucesso. É preciso abrir um tíquete de suporte para avisar o Google sobre aumento da carga? Não é necessário o chamado "pré-aviso".

A VPC oferece um conjunto de opções de balanceamento de carga. Se precisar de balanceamento de carga entre regiões para um aplicativo da Web, use o balanceamento de carga HTTP global. Para tráfego de secure socket layer que não seja HTTP, use o balanceador de carga de proxy SSL global. Se for outro tráfego TCP que não usa SSL, use o balanceador de carga de proxy TCP global. Os dois últimos serviços de proxy funcionam apenas para números de pool específicos e apenas para TCP. Se você quer balancear a carga do tráfego UDP ou de qualquer número de porta, ainda pode balancear a carga na região do Google Cloud com o balanceador de carga regional. Por fim, o que todos esses serviços têm em comum é que eles se destinam ao tráfego que entra na rede do Google pela Internet. Mas e se você quiser balancear a carga do tráfego dentro do seu projeto? Digamos, entre a camada de apresentação e a camada de negócios do seu aplicativo. Para isso, use o balanceador de carga interno regional. Ele aceita tráfego em um endereço IP interno do Google Cloud e faz o balanceamento de carga nas VMs do Compute Engine.
