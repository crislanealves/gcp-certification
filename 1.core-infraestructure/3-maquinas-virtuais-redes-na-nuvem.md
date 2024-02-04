
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

# Armazenamento na nuvem

# Opções de armazenamento do Google Cloud


Todos os aplicativos precisam armazenar dados, como mídia que será reproduzida por streaming ou até mesmo dados do sensor do dispositivo. Aplicativos e cargas de trabalho diferentes exigem soluções de bases de dados de armazenamento diferentes.

O Google Cloud tem opções de armazenamento para dados estruturados, não estruturados, transacionais e relacionais. Nesta seção, vamos conhecer os cinco produtos de armazenamento do Google Cloud: Cloud Storage, Cloud SQL, Cloud Spanner, Firestore e Cloud Bigtable.

Dependendo do seu aplicativo, você pode usar um ou vários desses serviços para alcançar seus objetivos.

# Cloud Storage

O Cloud Storage é um serviço que oferece aos desenvolvedores e às organizações em geral armazenamento de objetos duráveis e altamente disponível. 

O que é armazenamento de objetos? O armazenamento de objetos é uma arquitetura de armazenamento de dados de computador que gerencia os dados como objetos, e não como uma hierarquia de arquivos e pastas ou como blocos de um disco. Objetos são armazenados em um formato de pacote, que contém o formato binário dos dados, bem como metadados relevantes associados como a data da criação, o autor, o tipo de recurso e as permissões, além de um identificador global único.

Essas chaves exclusivas estão no formato de URLs, o que permite ao armazenamento de objetos interagir com tecnologias da Web facilmente. Dados normalmente armazenados como objetos são vídeos, imagens e gravações de áudio.

O Storage permite armazenar qualquer quantidade de dados e recuperá-los conforme necessário. É, também, um serviço escalonável totalmente gerenciado com diversos usos. Alguns exemplos incluem exibição de conteúdo de sites, armazenamento de dados para arquivos e recuperação de desastres e distribuição em downloads diretos de objetos grandes de dados para usuários.
 
O principal uso do Storage é o armazenamento de objetos binários grandes, ou BLOB, necessário para conteúdo on-line, como vídeos, fotos, dados de backup e arquivo etc. Os arquivos do Cloud Storage são organizados em buckets. 

Um bucket exige um nome globalmente exclusivo e uma localização geográfica específica onde deve ser armazenado. Um local ideal para um bucket é aquele com latência mínima, por exemplo, se a maioria dos seus usuários estiverem na Europa, convém escolher um local nesse continente ou uma região específica do Cloud na Europa ou na multirregião da União Europeia.
 
Os objetos de armazenamento oferecidos pelo Cloud Storage são imutáveis, ou seja, não é possível editá-los. Em vez disso, uma versão nova é criada quando uma mudança é feita. Os administradores têm a opção de permitir que cada versão substitua a outra por completo ou de manter o registro de cada mudança feita em um objeto específico ativando o controle de versões em um bucket.
 
Se você quiser usar o controle de versões, o Storage vai manter um histórico detalhado das modificações (substituições ou exclusões), de todos os objetos contidos no bucket. Se não ativar o controle de versões do objeto, versões novas sempre vão substituir as anteriores por padrão. Com o controle de versões do objeto, é possível listar as versões arquivadas de um objeto, restaura-lo  para um estado anterior ou excluir permanentemente uma versão, conforme necessário.
 
Na maioria dos casos, informações de identificação pessoal podem ser armazenadas em objetos de dados. Portanto, controlar o acesso aos dados armazenados é essencial para garantir a segurança e privacidade. Ao usar papéis do IAM e, quando necessário, listas de controle de acesso, as empresas podem cumprir as práticas recomendadas de segurança, que exigem que cada usuário tenha acesso e permissões apenas ao que precisa para as suas funções e não mais do que isso
 
Há algumas opções para controlar o acesso do usuário a objetos e buckets, mas na maioria dos casos o IAM é suficiente. Os papéis são herdados do projeto para o bucket até o objeto. Se você precisar de controle mais preciso, pode criar listas de controle de acesso. Cada lista consiste em duas informações:

- A primeira é um escopo que define quem pode acessar e realizar uma ação, podendo ser um usuário ou um grupo de usuários específico.
- A segunda é uma permissão que define quais ações podem ser realizadas, como leitura ou gravação.
 
Como armazenar e recuperar grandes quantidades de dados pode ser muito caro, o Cloud Storage também oferece políticas de gerenciamento de ciclo de vida. Por exemplo, você pode dizer ao Storage para excluir objetos com mais de 365 dias ou criados antes de 1º de janeiro de 2013, ou manter apenas as três versões mais recentes de cada objeto em um bucket com o controle de versões ativado. Ter esse controle garante que você não pague por mais do que realmente precisa.

## Cloud Storage: classes de armazenamento e transferência de dados


Há quatro classes primárias de armazenamento no Cloud Storage:

- A primeira é o Standard Storage. Ele é considerada o melhor para dados acessados frequentemente. Ele também é ótimo para dados armazenados por períodos curtos.
- A segunda é o Nearline Storage. Ele é melhor para armazenar dados pouco acessados que são lidos ou alterados uma vez por mês ou menos. Os exemplos incluem backups de dados, conteúdo multimídia de cauda longa ou arquivamentos de dados.
- A terceira classe é o Coldline Storage. Também é uma opção de baixo custo para armazenar dados pouco acessados. No entanto, em comparação ao Nearline Storage, o Coldline Storage é para dados lidos ou alterados no máximo uma vez a cada 90 dias.
- A quarta é o Archive Storage. Ele é a opção com menor custo, ideal para arquivamento de dados, backup on-line e recuperação de desastres. É ideal para dados que você pretende acessar menos de uma vez por ano, porque tem um custo maior de acesso aos dados e operações, além de uma duração mínima de armazenamento de 365 dias.
 
Embora cada classe tenha diferenças, muitas de suas características se aplicam a todas. Isso inclui armazenamento ilimitado sem tamanho mínimo de objeto, acessibilidade e localizações globais, latência baixa e alta durabilidade, experiência uniforme incluindo segurança, ferramentas e APIs, além de redundância geográfica se os dados estiverem em um local multirregional ou birregional. 

Servidores físicos são posicionados em data centers localizados em diversas regiões geográficas para proteger contra eventos catastróficos e desastres naturais e fazer o balanceamento de carga do tráfego para a melhor performance.
 
O Cloud Storage não tem tarifa mínima porque você paga apenas pelo que usa e o provisionamento prévio da capacidade não é necessário. De uma perspectiva de segurança, o Cloud Storage sempre criptografa os dados do lado do servidor antes de serem gravados no disco, sem custos adicionais.
 
O tráfego entre o dispositivo de um cliente e o Google é criptografado por padrão usando o protocolo HTTPS/TLS (Transport Layer Security). Independentemente da classe de armazenamento escolhida, há muitas maneiras de transferir seus dados para o Cloud Storage.
 
Muitos clientes fazem a própria transferência on-line usando a gsutil, que é a ferramenta de linha de comando do Cloud SDK do Cloud Storage. Os dados poderão ser enviados usando a opção de arrastar e soltar no Console do Cloud se o acesso for feito pelo navegador da Web Google Chrome.
 
Mas e se você precisar fazer upload de terabytes ou petabytes de dados? O Serviço de transferência do Storage permite importar grandes quantidades de dados on-line para o Cloud Storage de maneira rápida e econômica.
 
Com ele, é possível programar e gerenciar transferências em lote de um provedor de nuvem, de uma região do Cloud Storage diferente ou de um endpoint HTTP(S) para o Cloud Storage.
 
Também há o Transfer Appliance, que é um servidor de armazenamento em racks de alta capacidade que você aluga do Google Cloud. Você o conecta à sua rede, carrega com os dados e o envia para uma instalação de upload onde os dados são enviados para o Cloud Storage. É possível transferir até um petabyte de dados em um único dispositivo.
 
O Cloud Storage é totalmente integrado a outros produtos e serviços do Google Cloud, ou seja, há várias outras maneiras de mover dados para o serviço. Por exemplo, é possível importar e exportar tabelas de e para o BigQuery e o Cloud SQL. Você também pode armazenar logs do App Engine, backups do Firestore e objetos usados por aplicativos do App Engine, como imagens.
 
O Cloud Storage também armazena scripts de inicialização de instâncias, imagens do Compute Engine e objetos usados por aplicativos do Compute Engine.

## Cloud SQL


A segunda principal opção de armazenamento é o Cloud SQL. O Cloud SQL oferece bancos de dados relacionais totalmente gerenciados, incluindo MySQL, PostgreSQL e SQL Server como serviço.
 
Ele é projetado para delegar tarefas tediosas, mas necessárias, e que geralmente exigem muito tempo ao Google, como aplicar patches e atualizações, gerenciar backups e configurar replicações. Assim, você pode se concentrar em criar aplicativos incríveis. O Google Cloud SQL não requer instalação de software ou manutenção. Ele pode ser escalonado para até 64 núcleos de processador, mais de 400 GB de RAM e 30 TB de armazenamento. Ele oferece suporte a cenários de replicação automática, como de uma instância principal do Cloud SQL, uma instância principal externa e instâncias externas do MySQL.
 
O Cloud SQL oferece suporte a backups gerenciados, armazenando dados de backup com segurança e acessibilidade se for preciso restaurar. O custo de uma instância cobre sete backups. O Cloud SQL criptografa dados do cliente nas redes internas do Google e armazenados em tabelas de bancos de dados, arquivos temporários e backups. E ele inclui um firewall de rede, que controla o acesso da rede a cada uma das instâncias do banco de dados.
 
Um dos benefícios de instâncias do Cloud SQL é que elas são acessíveis por outros serviços do Google Cloud, bem como por serviços externos. O Cloud SQL pode ser usado com o App Engine usando drivers padrão como o Connector/J para Java ou o MySQLdb para Python.
 
Instâncias do Compute Engine podem ser autorizadas a acessar instâncias do Cloud SQL e é possível configurá-las para estar na mesma zona que sua máquina virtual. O Cloud SQL é compatível com aplicativos e ferramentas que você pode já usar, como SQL Workbench, Toad e outros aplicativos externos que usam drivers padrão do MySQL.

## Cloud Spanner

A terceira principal opção de armazenamento é o Cloud Spanner. O Cloud Spanner é um serviço de banco de dados relacional totalmente gerenciado que escalona horizontalmente, tem alta consistência e usa linguagem SQL. Testado na prática nos aplicativos e serviços essenciais do Google, o Spanner é o serviço que capacita os sistemas de US$ 80 bilhões do Google. O Cloud Spanner é especialmente adequado para aplicativos que exigem: um sistema de gerenciamento de banco de dados relacional SQL com mesclas e índices secundários alta disponibilidade integrada, alta consistência global, bancos de dados com mais de 2 TB e números altos de operações de entrada/saída por segundo. Estamos falando de dezenas de milhares de leituras/gravações ou mais por segundo.

## Firestore

A quarta principal opção de armazenamento do Google Cloud é o Firestore.

O Firestore é um banco de dados NoSQL na nuvem, flexível e com escalonamento horizontal para desenvolvimento da Web, dispositivos móveis e servidores. Com o Firestore, os dados são armazenados em documentos e organizados em coleções. Os documentos podem conter objetos aninhados complexos e subcoleções.

As consultas NoSQL do Firestore podem ser usadas para recuperar documentos individuais e específicos ou todos os documentos de uma coleção que correspondam aos parâmetros da consulta. As consultas podem incluir vários filtros conectados e combinar opções de filtragem e ordenação.

Elas também são indexadas por padrão. O desempenho da consulta é proporcional ao tamanho do conjunto de resultados e não ao conjunto de dados.

O Firestore usa sincronização para atualizar dados em qualquer dispositivo conectado. Mas ele também foi projetado para fazer consultas de busca simples e únicas de maneira eficiente.

Ele armazena em cache os dados ativamente usados por um app. Dessa maneira, o aplicativo pode gravar, ler, detectar e consultar dados, mesmo que o dispositivo esteja off-line. Quando o dispositivo volta a se conectar, o Firestore sincroniza todas as mudanças locais. O Firestore aproveita a infraestrutura poderosa do Google Cloud: replicação automática de dados em várias regiões, garantia de alta consistência, operações atômicas em lote e suporte real a transações.
 
Quanto aos preços, cada leitura, gravação e exclusão de documento que você fizer com o Firestore será cobrada. As consultas também são cobradas à taxa de uma leitura de documento por consulta, quer a consulta retorne dados ou não. Você também é cobrado pelo armazenamento que seus dados consomem e por determinados tipos de largura de banda de rede usada para acessar seus dados. Atualmente, a entrada é livre de custos e, em muitos casos, a saída também.
 
Consulte a página de preços do Firestore ou use a calculadora de faturamento do Google para estimar os preços para casos de uso específicos.
 
Além dos 10 GiB de saída de rede sem custos financeiros por mês entre as regiões dos EUA, o Firestore tem uma cota diária sem custos de 50 mil gravações de documentos, 20 mil exclusões de documentos e 1 GB de dados armazenados.
 
A cobrança só começa quando essa cota diária é excedida. Assim é possível começar a desenvolver com o Firestore por muito pouco ou até sem gastar nada.

## Cloud Bigtable

Cloud Bigtable é o serviço de banco de dados de Big Data NoSQL do Google.

É o mesmo banco de dados usado em vários serviços principais do Google, como Pesquisa, Analytics, Maps e Gmail. O Bigtable foi criado para lidar com cargas de trabalho grandes a uma latência sempre baixa e alta capacidade de processamento, o que o torna ideal para aplicativos de operações e análise, inclusive Internet das Coisas, análise de usuário e de dados financeiros. Ao decidir qual opção de armazenamento é a ideal, os clientes costumam escolher o Bigtable se: 

- trabalham com mais de 1 TB de dados semiestruturados ou estruturados, dados rápidos e alta capacidade de processamento ou que mudam muito rápido; 
- trabalham com dados NoSQL, normalmente, transações em que semânticas relacionais fortes não são necessárias, os dados são de séries temporais ou têm ordenação semântica natural;
- trabalham com Big Data, executam lotes assíncronos ou processamento síncrono em tempo real nos dados ou executam algoritmos de machine learning nos dados.

O Cloud Bigtable pode interagir com outros serviços do Google Cloud e clientes de terceiros. Ao usar APIs, os dados podem ser lidos e gravados no Cloud Bigtable por uma camada de serviço de dados, como VMs gerenciadas, o servidor REST HBase ou um servidor Java com o cliente HBase.

Isso geralmente é utilizado para exibir dados em aplicativos, painéis e serviços de dados.

Os dados podem ser transmitidos por streaming por diversos frameworks de processamento de stream, como o Dataflow Streaming, o Spark Streaming e o Storm.

Se o streaming não for uma opção, os dados poderão ser lidos e gravados no Cloud Bigtable por processos em lote, como o Hadoop MapReduce, o Dataflow ou o Spark.

Com frequência, dados resumidos ou recentemente calculados são gravados de volta no Cloud Bigtable ou em um banco de dados downstream.
