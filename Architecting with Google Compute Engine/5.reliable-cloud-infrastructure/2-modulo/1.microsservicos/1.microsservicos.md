# Microsserviços

Vamos começar analisando os detalhes de um microsserviço. Microsserviços dividem um programa grande em vários serviços independentes menores, ao contrário de um aplicativo monolítico, que implementa todos os recursos em uma única base de código com um banco de dados para todos os dados. Microsserviços são a tendência atual do setor, mas é importante ter um bom motivo para escolher essa arquitetura, um dos principais motivos é permitir que equipes trabalhem de forma independente. Isso suporta escalonar a organização, pois ter mais equipes aumenta a velocidade e, também, há o benefício de poder escalonar microsserviços independentemente, com base nos requisitos deles.

Quanto à arquitetura, um aplicativo projetado como um monolítico ou com base em microsserviços é composto de componentes modulares com limites claramente definidos. Com o monolítico, todos os componentes são empacotados no momento da implantação e implantados juntos

O Google Cloud fornece vários serviços de computação que facilitam a implantação de microsserviços, como o App Engine, o Cloud Run, o GKE e o Cloud Functions. Cada um deles oferece níveis de granularidade e controle diferentes.

Para serviços serem independentes, cada um deles precisa ter o próprio repositório de dados. Isso permite a melhor solução de armazenamento de dados para o serviço que será selecionado, e também mantém os serviços independentes. Não queremos introduzir acoplamento entre serviços por um repositório de dados. Uma arquitetura de microsserviços projetada corretamente ajuda a alcançar os objetivos a seguir:

- Definir contratos entre os diversos microsserviços.
- Permitir ciclos de implantação independentes, incluindo reversões.
- Facilitar testes A/B de lançamentos simultâneos em subsistemas.
- Minimizar automação de teste e sobrecarga de controle de qualidade.
- Melhorar a clareza da geração de registros e do monitoramento.
- Fornecer contabilidade dos custos detalhada.
- Aumentar a escalonabilidade geral do aplicativo e a confiabilidade com unidades de escalonamento menores.

Mas as vantagens precisam ser equilibradas com os desafios que esse estilo de arquitetura introduz. Alguns desses desafios incluem:

- Pode ser difícil definir limites claros entre serviços para dar suporte à implantação e ao desenvolvimento independentes.
- Maior complexidade da infraestrutura, com serviços distribuídos tendo mais pontos de falha.
- A latência maior introduzida pelos serviços de rede e a necessidade de criar resiliência para lidar com possíveis atrasos e falhas.
- Devido à rede envolvida, é necessário fornecer segurança para comunicação serviço a serviço, o que torna a infraestrutura mais complexa.
- Requisitos complexos para gerenciar e fazer a versão de interfaces com serviços implantáveis independentes.
- Maior necessidade de manter compatibilidade com versões anteriores.

Decompor aplicativos em microsserviços é um dos maiores desafios técnicos do design de aplicativos. Aqui, técnicas como design voltado a domínio são muito úteis para identificar agrupamentos funcionais lógicos.

A primeira etapa é decompor o aplicativo por recursos ou agrupamento funcional, a fim de minimizar dependências. Considere, por exemplo, um aplicativo de loja _on-line_. Agrupamentos funcionais lógicos podem ser: gerenciamento de produtos, análises, contas e pedidos. Esses agrupamentos compõem miniaplicativos, os quais expõem uma API. Cada um desses miniaplicativos será implementado, potencialmente, por vários microsserviços internamente. E esses microsserviços são organizados por camada de arquitetura, e cada um precisa ser escalonável e implantável independentemente.

As análises também vão identificar serviços compartilhados, como autenticação, que depois são isolados e implantados separadamente dos vários aplicativos. Ao projetar microsserviços, serviços que não retêm estados, mas os obtêm do ambiente ou dos serviços sem estado, são mais fáceis de gerenciar. Ou seja, são mais fáceis de escalonar, de administrar e de migrar para novas versões, porque não têm estado. Porém, geralmente não é possível evitar o uso de serviços com estado em algum ponto em um aplicativo com base em microsserviços. Portanto, é importante compreender as consequências de ter serviços com estado na arquitetura do sistema. Isso inclui introduzir desafios significativos na capacidade de escalonar e fazer upgrade dos serviços. É importante saber como o estado será gerenciado nos estágios iniciais do design do aplicativo de microsserviço. 

Na memória, o estado compartilhado tem implicações que afetam e negam muitos dos benefícios de uma arquitetura de microsserviços. O potencial de escalonamento automático de microsserviços individuais é atrasado porque solicitações posteriores do cliente precisam ser enviadas ao mesmo servidor em que a solicitação inicial foi feita. Adicionalmente, isso exige configurar os balanceadores de carga para usar sessões fixas, o que é chamado de afinidade da sessão no Google Cloud.

Uma prática recomendada para projetar serviços com estado é usar serviços de armazenamento de back-end compartilhados por serviços sem estado do front-end. Por exemplo, para estado permanente, os serviços de dados gerenciados pelo Google Cloud, como o Firestore ou Cloud SQL, podem ser úteis. Depois, para melhorar a velocidade do acesso aos dados, eles podem ser armazenados em cache. O Memorystore, que é um serviço com base em Redis altamente disponível, é ideal para isso.

Este diagrama mostra uma solução geral para a separação das etapas de processamento de front-end e back-end. Um balanceador de carga distribui a carga entre os serviços de back-end e front-end. Isso permite que o back-end escalone, se necessário, para acompanhar a demanda do front-end. Adicionalmente, os serviços ou os servidores com estado também são isolados. Os serviços com estado podem usar os serviços de armazenamento permanente e armazenamento em cache, como explicado anteriormente. Esse layout permite que uma grande parte do aplicativo use a escalonabilidade e a tolerância a falhas padrão dos serviços do Google Cloud como serviços sem estado. Isolando os serviços e servidores com estado, os desafios de escalonar e fazer upgrades ficam limitados a um subconjunto do conjunto geral dos serviços.

**Práticas Recomendadas de Microsserviços**

Vamos falar sobre práticas recomendadas para microsserviços. O "App de 12 fatores" é um conjunto de práticas recomendadas para criar aplicativos para a Web ou software como serviço. O projeto de 12 fatores ajuda a desacoplar componentes do aplicativo para que cada componente possa ser implantado na nuvem usando implantação contínua e escalonado verticalmente ou ter a escala vertical reduzida. Os princípios de projeto também maximizam a portabilidade para ambientes diferentes. Como os fatores são independentes de linguagens de programação ou de pilha de software, o projeto de 12 fatores pode ser aplicado em diversos tipos de aplicativos. Vamos ver essas práticas recomendadas.

**1. Base de Código:**
- A base de código precisa ser rastreada em um controle de versão, como o Git.
- Os Cloud Source Repositories fornecem repositórios privados com todos os recursos.

**2. Dependências:**
- As dependências precisam ser declaradas explicitamente e armazenadas em controle de versões.
- O rastreamento de dependências é feito com ferramentas específicas da linguagem, como Maven para Java e Pip para Python.
- Empacotar dependências em contêineres pode isolar o aplicativo.
- O Container Registry pode ser usado para armazenar as imagens e fornecer controle de acesso detalhado.

**3. Configuração:**
- Cada aplicativo tem uma configuração para cada ambiente, como de teste, de produção e de desenvolvimento.
- Essa configuração precisa ser externa ao código e manter variáveis de ambiente para flexibilidade da implantação.

**4. Serviços de Suporte:**
- Cada serviço de suporte, como banco de dados, cache ou mensagens, precisa ser acessado por URLs e definido pela configuração.
- Os serviços de suporte atuam como uma abstração para recursos subjacentes.
- O objetivo é poder trocar um serviço de suporte por uma implementação diferente com facilidade.

**5. Build, Lançamento e Execução:**
- O processo de implantação do software é dividido em três etapas: build, lançamento e execução.
- Cada etapa resulta em um artefato que tem uma identificação exclusiva.
- Isso permite fazer reversões facilmente e ter uma trilha de auditoria do histórico de cada implantação de produção.

**6. Processos:**
- Aplicativos são executados como um ou mais processos sem estado.
- Se um estado for exigido, a técnica discutida anteriormente neste módulo para gerenciamento de estados é a mais adequada.
- Cada serviço precisa ter os próprios armazenamentos de dados e cache, por exemplo, memória armazenada no cache e dados comuns compartilhados entre serviços usados.

**7. Vinculação de Portas:**
- Serviços são expostos usando um número de porta.
- O aplicativo empacota o servidor da Web como parte do aplicativo, não exigindo um servidor separado, como o Apache.
- No Google Cloud, esses apps podem ser implantados em serviços de plataforma, como o Compute Engine, o GKE, o App Engine ou o Cloud Run.

**8. Simultaneidade:**
- O aplicativo precisa ter a capacidade de escalonar horizontalmente, iniciando novos processos, e de retornar ao tamanho original para cumprir a demanda ou as cargas.

**9. Descartabilidade:**
- Aplicativos precisam ser escritos para ser mais confiáveis do que a infraestrutura em que são executados.
- Eles precisam ser capazes de lidar com falhas temporárias na infraestrutura subjacente e de desligar e reiniciar rapidamente.
- Aplicativos também têm que escalonar verticalmente e reduzir a escala vertical rapidamente, obtendo e lançando recursos conforme necessário.

**10. Paridade entre Desenvolvimento/Produção:**
- O objetivo é que os mesmos ambientes usados no desenvolvimento e no teste ou preparação sejam usados na produção.
- A infraestrutura como código e os contêineres do Docker facilitam isso.
- O Google Cloud oferece várias ferramentas que podem ser usadas para criar fluxos de trabalho que mantêm os ambientes consistentes.

**11. Registros:**
- Registros permitem ver a integridade dos aplicativos.
- É importante dissociar a coleta, o processamento e a análise de registros da lógica principal dos aplicativos.
- Os registros precisam ser gerados como uma saída padrão e agregados em uma só fonte.

**12. Processos do Administrador:**
- Geralmente, os processos do administrador são realizados uma vez e precisam estar desacoplados do aplicativo.
- Eles precisam ser automatizados e reproduzíveis, em vez de processos manuais.
- No Google Cloud, há várias opções para fazer isso, incluindo cron jobs no GKE, tarefas de nuvem no App Engine e o Cloud Scheduler.