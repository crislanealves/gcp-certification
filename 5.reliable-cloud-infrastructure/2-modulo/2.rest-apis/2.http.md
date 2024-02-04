# HTTP

Um cliente acessa formulários de serviço HTTP e solicitações de HTTP. Solicitações HTTP são criadas em três partes: a linha da solicitação, as variáveis de cabeçalho e o corpo da solicitação. A linha da solicitação tem o verbo HTTP, GET, POST, PUT etc., bem como o URI solicitado e o protocolo da versão. As variáveis de cabeçalho contêm pares de chave-valor. Alguns são padrões, como agente do usuário, que ajuda o destinatário a identificar o agente de software solicitante. Metadados sobre o formato da mensagem ou os formatos da mensagem preferidos também são incluídos aqui para os serviços REST baseados em HTTPS. É possível adicionar cabeçalhos personalizados.

O corpo da solicitação contém dados que serão enviados para o servidor e é relevante apenas para comandos HTTP que enviam dados, como POST e PUT. Aqui, vemos dois exemplos de mensagens com base em texto do cliente HTTP. O primeiro exemplo mostra uma solicitação HTTP GET para o URL usando HTTP versão 1.1. Há uma variável de cabeçalho de solicitação chamada "host" com o valor `pets.drehnstrom.co`. O segundo exemplo mostra uma solicitação HTTP POST para o URL /add usando HTTP versão 1.1. Há três variáveis de cabeçalho de solicitação: host; tipo de conteúdo, definido como JSON; e comprimento do conteúdo, definido como 35 bytes. Há um corpo de solicitação, que tem o documento JSON, `{name: Noir, breed: Schnoodle}`. Isso representa o pet sendo adicionado.

Como parte de uma solicitação, o verbo HTTP diz para o servidor qual ação realizar em um recurso. HTTP como um protocolo fornece nove verbos, mas, geralmente, apenas os quatro listados aqui são usados no REST.

- **GET** é usado para recuperar recursos. 
- **POST** é usado para solicitar a criação de um novo recurso. Então, o serviço cria o recurso e geralmente retorna o ID exclusivo gerado do novo recurso ao cliente. 
- **PUT** é usado para criar um novo recurso ou alterar um recurso existente. A solicitação PUT precisa ser idempotente, ou seja, não importa quantas vezes a solicitação seja feita pelo cliente a um recurso, os efeitos do recurso sempre são exatamente os mesmos; e, por fim,
- **DELETE** é usada para remover um recurso.

Serviços HTTP retornam respostas em um formato padrão definido por HTTP. Essas respostas HTTP são criadas em três partes: a `linha da resposta`, as `variáveis de cabeçalho` e o `corpo da resposta`:

- A linha da resposta tem a versão do HTTP e um código de resposta. Os códigos de resposta são divididos em limites na casa de centenas. O intervalo 200 significa OK. Por exemplo, 200 é OK, 201 quer dizer que um recurso foi criado. O intervalo 400 significa que a solicitação do cliente tem um erro. Por exemplo, 403 significa "proibido" porque a solicitação não tem permissão. 404 significa que o recurso não foi encontrado. O intervalo 500 significa que o servidor encontrou um erro e não pode processar a solicitação. Por exemplo, 500 é o "erro interno do servidor". 503 quer dizer "não disponível", geralmente porque o servidor está sobrecarregado.

- O cabeçalho da resposta é um conjunto de pares de chave-valor, como tipo de conteúdo, que indica para o destinatário o tipo de conteúdo contido no corpo da resposta. 
    
- O corpo da resposta contém uma representação de recurso solicitada no formato especificado no cabeçalho de tipo de conteúdo, e pode ser JSON, XML, HTML etc. As diretrizes listadas aqui focam em alcançar consistência na API. Substantivos singulares precisam ser usados para recursos individuais, e substantivos plurais, para coleções ou conjuntos. Por exemplo, considere o seguinte URI /pet. Então, uma solicitação GET para o URI /pet/1 busca um pet com o ID 1, já GET/pets busca todos os pets. Não use URIs como GET/GETpets. **O URI precisa referenciar o recurso, e não a ação no recurso**. Esse é o papel do verbo. Lembre-se que URIs não diferenciam maiúsculas de minúsculas e incluem informações da versão.
