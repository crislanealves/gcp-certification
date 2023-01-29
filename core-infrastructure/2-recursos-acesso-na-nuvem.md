## Recursos e acesso na nuvem

# **Hierarquia de recursos do Google Cloud**

A hierarquia de recursos do Google Cloud tem 4 níveis, de baixo para cima, eles são: recursos, projetos, pastas e organização.:

![image](https://user-images.githubusercontent.com/58278652/215269983-aac4e79c-77ce-4770-b788-a308a4e28a9b.png)


**Recursos:**

No primeiro nível estão os recursos. Eles representam serviços como máquinas virtuais, buckets no Storage, tabelas no BigQuery ou outro elemento no Google Cloud. Recursos são organizados em projetos, que são o segundo nível.

**Projetos:**

Idealmente os projetos são organizados em pastas/subpastas, apesar de não ser obrigatório a existência de pastas para criação de um projeto. 

No entanto, é obrigatório a existencia de um projeto para utilizar a maioria dos recursos dentro do GCP. Os projetos viabilizam o uso dos serviços do Google Cloud, como o gerenciamento de APIs, faturamento, adição e remoção de colaboradores e muitos outros serviços.

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

Você também pode usar o Cloud Identity, a plataforma de gerenciamento de identidade, para criar uma organização. Quando criada, a organização permite que qualquer pessoa no domínio crie projetos e contas de faturamento. Também é possível criar e incluir projetos em pastas abaixo da organização;
Pastas e projetos são considerados filhos da organização.

É importante entender essa hierarquia porque ela se relaciona com as políticas aplicadas no Google Cloud. Essas políticas podem ser definidas no nível do projeto, da pasta e da organização. Alguns serviços do Google Cloud permitem aplicar políticas a recursos individuais.



