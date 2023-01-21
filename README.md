- Certificação Google Cloud Associate Engineer (GCP)

## História sobre a Google Cloud Platform:

1. Em 2008 a Google começa a desenvolver/utilizar alguns serviços para consumo próprio, ou seja, para resolver problemas internos. Posteriormente, mais especificamente em 2011, eles entendem que outras organizações podem demandar das mesmas soluções que eles criaram internamente e, então, eles abrem esses serviços para o público, e a partir daí começam a ganhar tração mundial.

2. O GCP é a mais nova das grandes clouds do mercado. 

## Zonas, Região e Network:

x. A hierarquia de localização da Google segue e estrutura: Globo > Multi-Região > Região > Zona. Dentro de cada zona tem os data centers que são os complexos onde toda a parte computacional mora.

	Globo: Mapa Mundi
	Multi-região: onde moram várias regiões/zonas
	Região: São coleções de zonas. 
	Zona: É uma área de implantação em uma região. 
	
x. Em resumo, um grupo de zonas formam uma região e um grupo de regiões formam uma multi-região.

x. As zonas têm conexões de rede de alta largura de banda e baixa latência com outras zonas na mesma região. 

	- Largura de banda: quanto maior a largura de banda, maior será a velocidade de uma conexão.
	
	- Baixa latência: é um conceito sobre o tempo de resposta. Nesse caso, é o tempo gasto para uma mensagem ir de um ponto para o outro. Por exemplo, quando solicitamos uma informação de um data center, o tempo que leva para ele responder é chamado de latência. Sendo assim, o melhor é que ocorra uma baixa latência, pois os dados serão enviados rapidamente para quem os está requisitando.
	

x. Para implantar aplicativos tolerantes a falhas que tenham alta disponibilidade, o Google recomenda a implantação de aplicativos em várias zonas e regiões. Isso ajuda na proteção contra falhas inesperadas de componentes, incluindo até uma única zona ou região.

	- Alta disponibilidade: é a capacidade de garantir que a conexão seja utilizada sem nenhuma interrupção, seja por falta de energia, por problemas no hardware ou no softwarte.

x. Escolha regiões que façam sentido para seu cenário. Por exemplo, se você só tiver clientes nos EUA ou se tiver necessidades específicas que exijam que seus dados estejam nos EUA, faz sentido armazenar os recursos em zonas das regiões us-central1 ou us-east1, por exemplo.

x. Nomenclatura de região e zona: 
	Região: us-east1
	Zona: us-east1-a, us-east1-b, us-east1-c

x. Os recursos regionais podem ser usados por quaisquer recursos na região, independente da zona. 

x. Os recursos de zona só podem ser usados por recursos na mesma zona.

x. Colocar recursos em diferentes zonas de uma região reduz o risco de interrupção da infraestrutura que afeta todos os recursos simultaneamente. Já a distribuição entre diferentes regiões garante um nível ainda mais elevado de independência em relação a falhas. Isso permite projetar sistemas robustos com recursos espalhados por diferentes domínios de falhas.

x.As sub-redes se estendem por zonas em uma região. Isso é exclusivo do Google Cloud e diferente dos demais fornecedores. Com isso, é mais fácil criar confiabilidade porque instâncias adjacentes podem estar em zonas diferentes na mesma sub-rede, permitindo o isolamento de falhas.

x. Toda estrutura de Network (redes, cabos físicos) da Google são privados, ou seja, pertecem a Google. 

Referencias:

[Benefícios da Alta Disponibilidade e Baixa Latência](
https://ascenty.com/blog/artigos/beneficios-da-alta-disponibilidade-e-baixa-latencia/#:~:text=J%C3%A1%20a%20baixa%20lat%C3%AAncia%20%C3%A9,responder%20%C3%A9%20chamado%20de%20lat%C3%AAncia)


## Hierarquia de recursos


x. Os recursos do Google Cloud são organizados hierarquicamente. A Hierarquia de recursos dentro do GCP, segue a estrutura: Organização > Pastas > Projetos > Recursos.

![image](https://user-images.githubusercontent.com/58278652/210765098-be5afb51-c998-48b1-989b-aaabf8d2b9e5.png)


	- Organização: é o topo da hierarquia de recursos do Google Cloud. Não é obrigatória apesar de que alguns recursos do Resource Manager não poderão ser usados sem uma.


	- Pastas: São um mecanismo de agrupamento adicional e opcional entre os recursos da organização e do projeto. É obrigatório ter uma organização para usar pastas (ou seja, só é possível criar pastas dentro de organizações).
	
	- Projetos:  É a entidade organizadora de nível base. Organização e pastas podem conter vários projetos. É necessário ter um projeto para:
	
		- Usar o Google Cloud Platform
		- Formar a base para criar, ativar e usar todos os serviços do Google Cloud
		- Gerenciar APIs, ativar o faturamento, adicionar e remover colaboradores e gerenciar permissões.
	

x. Você pode criar projetos sem vincula-los a uma Organização.

x. O ponto positivo de seguir a estrutura organizacional de recursos da Google, é facilitar alguns pontos como, por exemplo:

	  - Melhorar organização geral.
	  - Mais fácil de conceder acessos:
		- É possível definir roles especificas para cada pasta/projetos.
	  - Mais fácil de controlar faturamento:
		- É possivel criar uma conta (ou configurar um orçamento) e associar ela a uma pasta/projeto ou serviço especifico.
		
x. É possível migrar recursos de projetos. 

x. A hierarquia de recursos do Google Cloud, principalmente na forma mais completa que inclui recursos de organização e de pasta, permite que:
	- As empresas mapeem a organização para o Google Cloud.
	- Fornece pontos lógicos de anexos para políticas de gerenciamento de acesso (IAM) e políticas da organização. 

x. O Google Cloud oferece o IAM, que permite atribuir acesso granular a recursos específicos e impede o acesso indesejado a outros recursos. Por meio da definição de políticas do IAM, é possível controlar quem (usuários) tem que tipo de acesso (papéis) a quais recursos.

x. É possível definir uma política do IAM no nível da organização, no nível da pasta, no nível do projeto ou, em alguns casos, no nível do recurso. 

x. As políticas do IAM e da organização são herdadas pela hierarquia.

x. A política vigente para cada recurso na hierarquia é o resultado das políticas aplicadas diretamente ao recurso e daquelas herdadas dos ancestrais dele.


Referencias:

- [Hierarquia](https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=pt-br)

- [Migrar recursos de projetos](https://cloud.google.com/resource-manager/docs/project-migration?hl=pt-br)


## IAM

x. Uma política é definida em um recurso, e cada política contém uma série de papéis e membros. Os recursos herdam as políticas das instâncias primárias. Então uma política pode ser definida em um recurso, como um serviço, e outra política pode ser criada em uma instância primária, como um projeto que contém aquele serviço. A política final é a união da política primária e da política do recurso. 

x. O que acontece quando essas duas políticas estão em conflito? E se a política no recurso conceder acesso a apenas um único bucket do Cloud Storage e restringir o acesso a todos os outros buckets? Porém, no nível do projeto, há uma regra que dá acesso a todos os buckets no projeto. Qual regra vence? **A mais restritiva no recurso ou a mais geral no projeto?** **Se uma política primária é menos restritiva, ela substitui a mais restritiva do recurso**. **Nesse caso, a política do projeto vence**.


## Google CLoud Shell

Referencias 

Visão geral da CLI gcloud: https://cloud.google.com/sdk/gcloud?hl=pt-br

Gcloud | cheat-sheet: https://cloud.google.com/static/sdk/docs/images/gcloud-cheat-sheet.pdf

Gcloud | cheat-sheet 2 :https://mishnit.github.io/cheatsheet-gcp-A4.pdf

## Google Storage 

x. É o primeiro serviço da Google Cloud.

x. Armaneza objetos (videos, imagens, dataframes).

x. Classes de armazenamento Google Cloud:

	- Standard: Acessado com muita frequencia. É a classe mais cara de armazenamento
	- Nearline: Armazenamento de arquivo que serão acessado após 30 dias. Baixo custo. 
	- Coldline: Armazenamento de arquivo que serão acessado após 90 dias. Mais barato que o primeiro e o segundo.  
	- Archive: Armazenamento de arquivo que serão acessado após 365 dias. O mais barato de todos. 

As recomendações de dias são feitas por conta do sistema retrieval. Retrieval em poucas palavras é o custo da movimentação do arquivo. Por exemplo, objetos armazenados na classe standard tem um retrieval alto, já em archive o retrieval é baixo. O valor no archive é mais baixo já que, uma vez que a movimentação é baixa, o Google Cloud armazenará esses arquivos em uma localização mais barata, um data center mais barato, com hardware mais barato. 

O Cloud Storage é persistente. Você já deve conhecer os métodos de controle de acesso granular do Storage, como os papéis do IAM e os URLs assinados. O Cloud Storage tem muitos recursos que as pessoas não conhecem. Muita gente acaba duplicando a função no código quando deveria usar o recurso que já está disponível. Por exemplo, mudança da classe de armazenamento, streaming, controle de versões e várias opções de criptografia. Você também pode automatizar alguns recursos usando o gerenciamento de ciclo de vida. Por exemplo, alterar a classe de armazenamento de um objeto ou excluir o objeto após um período.


## BigQuery

x. O BigQuery é chamado de armazenamento em colunas, ou seja, ele foi projetado para processar colunas, não linhas. 

x. O processamento de colunas é barato e rápido, e o processamento de linhas é lento e caro. 

x. A maioria das consultas funciona apenas em um pequeno número de campos, e o BigQuery só precisa ler as colunas relevantes para executar uma consulta. Como cada coluna tem dados do mesmo tipo, o BigQuery pode compactar os dados da coluna com muito mais eficiência.

## Cloud SQL

O Cloud SQL é o serviço gerenciado que oferece instâncias do MySQL. Há várias formas de criar conexões seguras com instâncias do Cloud SQL. É importante conhecer as diversas abordagens e vantagens que elas oferecem. O Cloud SQL é adequado para quem não precisa de mais de um banco de dados.

## Cloud Bigtable

O Cloud Bigtable serve para dados de alta capacidade. A latência dele é de alguns milissegundos, muito mais rápido que o BigQuery. Por ser NoSQL, ele é ideal para armazenar dados em colunas. Quando você usaria um SSD para as máquinas no cluster em vez de HDD? Quando você precisasse de mais velocidade.
As tabelas do Bigtable são altas e estreitas. Este exemplo mostra uma ação da bolsa em cada linha. O resultado serão milhões de linhas por dia, o que não é um problema para o Bigtable. 


## Cloud Spanner

x. O Cloud Spanner tem tipo forte e consistência global. O que o diferencia do Cloud SQL é a consistência das transações e o tamanho. O Cloud Spanner trabalha com bancos de dados muito maiores que o Cloud SQL.

x. O Cloud Spanner é uma ótima opção para quem precisa de vários bancos de dados. O MySQL tem um limite de desempenho. Observando o 99º percentil de latência, está claro que o desempenho cai. Distribuir o MySQL é difícil. Já o Spanner tem uma distribuição fácil e global, além de permitir adicionar mais nós para aumentar a capacidade e manter o desempenho consistente.

## Cloud Datastores

O Cloud Datastore é uma solução NoSQL que era exclusiva do App Engine. Ele tem recursos úteis para aplicativos, como informações de persistência de estado. E agora está disponível para outros clientes além do App Engine.





