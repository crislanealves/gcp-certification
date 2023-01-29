# Recursos e acesso na nuvem

## **Hierarquia de recursos do Google Cloud**

A hierarquia de recursos do Google Cloud tem 4 níveis, de baixo para cima, eles são: recursos, projetos, pastas e organização.:

![image](https://user-images.githubusercontent.com/58278652/215269983-aac4e79c-77ce-4770-b788-a308a4e28a9b.png)


**Recursos:**

No primeiro nível estão os recursos. Eles representam serviços como máquinas virtuais, buckets no Storage, tabelas no BigQuery ou outro elemento no Google Cloud. Recursos são organizados em projetos, que são o segundo nível.

**Projetos:**

Idealmente os projetos são organizados em pastas/subpastas, apesar de não ser obrigatório a existência de pastas para criação de um projeto. No entanto, é obrigatório a existencia de um projeto para utilizar a maioria dos recursos dentro do GCP. Os projetos viabilizam o uso dos serviços do Google Cloud, como o gerenciamento de APIs, faturamento, adição e remoção de colaboradores e muitos outros serviços.

Cada projeto é uma entidade separada na organização e cada recurso pertence a apenas um projeto. Eles têm vários proprietários e usuários pois são faturados e gerenciados separadamente. 

Cada projeto tem três atributos de identificação: ID, nome e número do projeto.
O ID do projeto é um identificador exclusivo global que não pode ser alterado após a criação, ele é imutável. Os IDs do projeto são usados para informar ao Google Cloud em qual projeto trabalhar. Já os nomes dos projetos são criados pelo usuário. Eles podem ser alterados a qualquer momento, ou seja, são mutáveis.

O Google Cloud também atribui um número exclusivo a cada projeto. Eles são usados internamente para rastrear os recursos. A ferramenta de gestão de recursos foi criada para gerenciar projetos programaticamente. É uma API que coleta uma lista de todos os projetos associados a uma conta, cria novos projetos, atualiza os projetos existentes e exclui projetos. Ela também recupera projetos que foram excluídos e podem ser acessados pela API RPC e pela API REST.

**Pastas:**

O terceiro nível da hierarquia de recursos são as pastas. Elas permitem atribuir políticas no nível de granularidade que você quiser. Os recursos em uma pasta herdam as políticas e permissões atribuídas a ela. 

Uma pasta pode conter projetos, outras pastas ou uma combinação de ambos.
Por exemplo, sua organização pode ter vários departamentos, cada um com o próprio conjunto de recursos. Com as pastas, é possível agrupar os recursos por departamento.

Utilizando pastas as equipes podem delegar direitos administrativos para trabalharem com independência. Os recursos em uma determinada pasta herdam as políticas e as permissões atribuídas, ou seja, se você aplicar uma política a uma pasta ela vai ser aplicada a todos os projetos da pasta. Então, se você tiver dois projetos distintos administrados pela mesma equipe, pode colocar as políticas na mesma pasta para conceder permissões.

Para usar as pastas, você precisa de uma a organização, já que tudo que está ligado à conta fica dentro da organização, o que inclui pastas, projetos e outros recursos.

**Organização:**

No nível superior, está a organização, que inclui todos os projetos, pastas e recursos da sua organização.

Existem papéis especiais associados à organização. É possível designar o papel de Administrador de políticas da organização e só pessoas com esse papel podem alterar as políticas. Tem também o papel de Criador de projetos que é bom para controlar quem pode criar projetos e fazer gastos.

Você também pode usar o Cloud Identity, a plataforma de gerenciamento de identidade, para criar uma organização. Quando criada, a organização permite que qualquer pessoa no domínio crie projetos e contas de faturamento. Também é possível criar e incluir projetos em pastas abaixo da organização.
Pastas e projetos são considerados filhos da organização.

É importante entender essa hierarquia porque ela se relaciona com as políticas aplicadas no Google Cloud. Essas políticas podem ser definidas no nível do projeto, da pasta e da organização. Alguns serviços do Google Cloud permitem aplicar políticas a recursos individuais.

## Identity Access Management (IAM)

Quando o nó da organização tem muitas pastas, projetos e recursos, é necessário restringir quem tem acesso ao quê, a ferramenta do IAM trata justamente desses casos. Com o IAM, é possível aplicar políticas que definem quem pode fazer o quê e em quais recursos. O "quem" da política do IAM pode ser uma Conta ou Grupo do Google, uma conta de serviço ou um domínio do Cloud Identity. 

O tipo de papel define o que cada um pode fazer (um papel é um conjunto de permissões). Por exemplo, para gerenciar as instâncias de uma máquina virtual em um projeto, você precisa poder criar, excluir, iniciar, interromper e alterar as máquinas virtuais. Essas permissões são agrupadas em um papel, facilitando a compreensão e o gerenciamento. Se um usuário, grupo ou conta de serviço tem um papel em um elemento específico da hierarquia do recurso, ele se aplica ao elemento escolhido e aos elementos abaixo dele na hierarquia. 

Há três tipos de papéis no IAM: básico, predefinido e personalizado. Os papéis básicos têm um escopo amplo, quando aplicados a um projeto, eles afetam todos os recursos do projeto. Os papéis básicos incluem proprietário, editor, leitor, administrador de faturamento, etc. Leitores podem acessar recursos, mas sem fazer alterações. Editores podem acessar e fazer alterações. Proprietários podem acessar e fazer alterações em um recurso, além de poderem gerenciar papéis e permissões associados e configurar o faturamento. Muitas empresas querem que o responsável pelo controle do faturamento não tenha permissão para alterar os recursos, por isso existe o papel de Administrador de faturamento.

**Um ponto de atenção:** em projetos com várias pessoas e dados confidenciais, papéis básicos são amplos demais. O Cloud IAM fornece outras maneiras de atribuir permissões personalizadas especificamente para atender às necessidades do projeto. Isso nos leva ao segundo tipo de papel, o predefinido.

Serviços específicos oferecem conjuntos de papéis predefinidos e indicam quando eles podem ser aplicados. É possível aplicar papéis predefinidos específicos, como “instanceAdmin”, aos recursos do Compute Engine em um projeto, pasta ou em toda a organização. Isso permite que quem tiver esse papel pode executar um conjunto específico de ações predefinidas.

E caso seja necessário atribuir um papel com permissões mais específicas? Daí você vai usar o papel personalizado. Muitas empresas usam o modelo de privilégio mínimo, em que cada pessoa tem o mínimo de privilégios necessários para trabalhar. Talvez você queira definir um papel de "Operador de instâncias" para permitir que alguns usuários iniciem e interrompam máquinas virtuais, por exemplo, mas sem poder reconfigurá-las. Você pode definir as permissões com papéis personalizados.

**Dois detalhes são importantes:**

Primeiro, é preciso gerenciar as permissões que definem o papel personalizado. Por isso, algumas organizações preferem usar os papéis predefinidos.

Segundo, esses papéis só podem ser aplicados no nível do projeto ou da organização. Eles não podem ser aplicados no nível da pasta.

## Contas de serviço 

E se você quiser conceder permissões personalizadas a uma VM em vez de uma pessoa? As contas de serviço são para isso.

Imagine que um aplicativo da sua VM precisa armazenar dados no Cloud Storage e você não quer que ninguém tenha acesso aos dados, apenas uma VM em particular. É possível criar uma conta de serviço para autenticar a VM no Cloud Storage.

Contas de serviço têm endereço de e-mail, mas em vez de senhas elas usam chaves criptográficas.

Se uma conta de serviço tem o papel de administrador da instância do GCE, isso permite que o aplicativo com a conta de serviço crie, modifique ou exclua outras VMs.

Além disso, contas de serviço precisam ser gerenciadas. Talvez Alice precise gerenciar qual conta pode agir como conta de serviço, enquanto Bob precisa apenas ver uma lista de contas de serviço. Além de ser uma identidade, uma conta de serviço também é um recurso. Então ela pode ter as próprias políticas do IAM.

Isso significa que Alice pode ter o papel de editor e Bob o papel de leitor. É como conceder papéis para qualquer outro recurso do Google Cloud.

## Cloud Identity 

Quando um novo cliente começa a usar a plataforma, ele faz o login no Console do Google Cloud com uma conta do Gmail e usa os Grupos do Google para colaborar com colegas de equipe.

Esse método é fácil no início, mas pode gerar alguns desafios porque as identidades não são gerenciadas centralmente. Isso pode ser problemático se alguém deixar a organização. Com essa configuração não há maneira fácil de remover imediatamente o acesso do usuário.

Com a ferramenta Cloud Identity, as organizações podem definir políticas e gerenciar usuários e grupos usando o Google Admin Console.

Administradores podem fazer login<b> </b>e gerenciar recursos com os nomes de usuário e senhas que já utilizam nos sistemas LDAP ou Active Directory existentes.

Usando o Cloud Identity, quando alguém deixa a organização, o administrador pode desativar a conta do usuário e removê-la dos grupos.

O Cloud Identity está disponível em uma versão sem custos e uma premium com funcionalidades para dispositivos móveis. Se você é um cliente do Google Cloud e também do Google Workspace, ela já está disponível para você no Google Admin Console.

## Interação com o Google Cloud

Há 4 maneiras de acessar e interagir com o Google Cloud: o Console do Cloud, o SDK Cloud e o Cloud Shell, as APIs e o app Console do Cloud para dispositivos móveis. Vamos explorar cada uma delas.

A primeira é o Console do Google Cloud, uma interface gráfica do usuário que ajuda você a implantar, escalonar e diagnosticar problemas na produção em uma interface baseada na Web.

Com o Console do Cloud, você encontra facilmente seus recursos, verifica a integridade deles, controla o gerenciamento e define orçamentos para controlar os gastos. O Console também tem um mecanismo de pesquisa para encontrar recursos e se conectar a instâncias via SSH no navegador.

A segunda maneira é pelo SDK Cloud e o Cloud Shell. O SDK Cloud tem ferramentas para gerenciar recursos e aplicativos hospedados no Google Cloud. Ele tem a ferramenta gcloud, que fornece a principal CLI de produtos e serviços do Google Cloud, gsutil, que permite o acesso ao Cloud Storage a partir da linha de comando e bq, uma ferramenta de linha de comando para o BigQuery.

Todas as ferramentas instaladas no SDK Cloud ficam no diretório bin.

O Cloud Shell concede acesso a recursos usando a linha de comando diretamente do navegador. Ele é uma máquina virtual baseada em Debian com diretório principal permanente de 5 GB. Isso facilita o gerenciamento de projetos e recursos. Com o Cloud Shell, você tem a ferramenta gcloud do SDK Cloud e outros utilitários sempre instalados, disponíveis, atualizados e totalmente autenticados.

A terceira maneira de acesso é pela interface de programação do aplicativo, ou API. Os serviços que compõem o Google Cloud oferecem APIs, para você controlar o ambiente usando código. O Console tem uma ferramenta chamada APIs Explorer do Google que mostra quais APIs estão disponíveis e as versões. Você pode testar essas APIs, mesmo as que exigem autenticação do usuário.

Imagine que você testou uma API e está pronto para criar um aplicativo. É preciso programar do zero? Não. O Google oferece bibliotecas de cliente do Cloud e bibliotecas de cliente de APIs do Google em várias linguagens para eliminar o trabalho árduo de chamar o Google Cloud com o código. As linguagens representadas atualmente nessas bibliotecas são Java, Python, PHP, C#, Go, Node.js, Ruby e C++ .

A quarta maneira de acessar e interagir com o Google Cloud é com o Console do Cloud para dispositivos móveis, que pode ser usado para iniciar, interromper e usar o SSH para se conectar a instâncias do Compute Engine e ver os registros delas. Com ele você inicia e para instâncias do Cloud SQL. Além disso, você pode administrar aplicativos implantados no App Engine, visualizar erros, reverter implantações e alterar a divisão de tráfego.

O app Console do Cloud oferece informações de faturamento atualizadas e alertas para projetos que excedem o orçamento. Também é possível configurar gráficos com as principais métricas, como uso de CPU, uso de rede, solicitações por segundo e erros de servidor. O app também oferece alertas e gerenciamento de incidentes. 
