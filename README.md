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
