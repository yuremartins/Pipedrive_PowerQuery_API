![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

<h1 align="center"> Projeto com API - Pipedrive integrado ao Excel através do Power Query </h1>

Este projeto tem como objetivo criar uma integração eficiente entre o Pipedrive, um popular CRM, e o Power Query, uma poderosa ferramenta de consulta e transformação de dados disponível no Excel e no Power BI.

Existem diferentes formas de extrair dados de um CRM e enviá-los para uma ferramenta de Business Intelligence, como o Power BI. No entanto, fazer isso manualmente através de exportação em CSV pode ser trabalhoso e demorado. Além disso, a utilização de conectores de terceiros pode ser custosa e limitante.

Neste projeto, vamos explorar a integração do Pipedrive com o Power Query através da API. Utilizando a linguagem M do Power Query, iremos extrair dados do Pipedrive e carregá-los no Power BI, permitindo a criação de relatórios e painéis interativos.

As principais funcionalidades desse projeto incluem:

- Obtendo as Credenciais:
Para começar, é necessário obter suas credenciais de autenticação. Você precisará do seu Token de API do Pipedrive e a URL base da API. Explicaremos como obter essas informações e garantir que você esteja autorizado a fazer chamadas à API do Pipedrive.

- Configurando Parâmetros:
Ao usar o Power Query, é comum utilizar parâmetros para permitir maior flexibilidade nas consultas. Vamos mostrar como configurar parâmetros para especificar filtros, datas e outras opções relevantes para suas consultas específicas.

- Endpoints e suas Funcionalidades:
A API do Pipedrive possui uma variedade de endpoints que permitem acessar diferentes tipos de dados, como negócios, pessoas, atividades e mais. Explicaremos os principais endpoints disponíveis, suas funcionalidades e os parâmetros que podem ser utilizados para refinar suas consultas.

- Criação do Script em Linguagem M:
O Power Query utiliza a linguagem M para criar consultas personalizadas. Mostraremos como escrever um script em linguagem M para fazer chamadas à API do Pipedrive, utilizar os parâmetros configurados e obter os dados desejados. Também abordaremos como manipular e transformar os resultados para atender às suas necessidades.

- Combinando Endpoints no Excel:
Uma das vantagens do Power Query é a capacidade de combinar múltiplos endpoints em uma única consulta. Vamos demonstrar como combinar dados de diferentes endpoints para obter uma visão mais completa e consolidada do seu CRM

Este projeto é especialmente útil para empresas que desejam integrar seus dados do Pipedrive ao Power BI de forma automatizada e personalizada. Ao utilizar a API do Pipedrive em conjunto com o Power Query, você terá acesso completo ao banco de dados do seu CRM e poderá explorar as informações de maneira flexível e eficiente.

Ao finalizar este projeto, você estará apto a conectar o Pipedrive ao Power BI de forma automatizada, permitindo análises avançadas e tomadas de decisão embasadas em dados atualizados e precisos."

A partir deste ponto, podemos continuar com os próximos passos do projeto.


## Parâmetros
### Criação dos Paramêtros:
O primeiro passo é criar dois parâmetros no Power BI que serão utilizados como referência para suas consultas. Essa etapa é importante para garantir a flexibilidade e facilidade de atualização, caso a URL ou o token de acesso do Pipedrive sejam alterados. Siga as etapas abaixo:

- Acesse o ambiente de transformação de dados no Power BI e vá para "Gerenciar Parâmetros".
- Crie um novo parâmetro para a URL da sua conta no Pipedrive e outro parâmetro para o token do Pipedrive. Ambos devem ser do tipo texto.

### Obtendo o Token e URL do Pipedrive:
Obtendo o Token e URL do Pipedrive:
Para obter o token de acesso e a URL do Pipedrive, siga as instruções abaixo:

- Acesse as configurações da sua conta no Pipedrive.
- Clique no canto superior direito, na imagem do usuário, e selecione "Ajustes".
- Em seguida, vá para "Preferências Pessoais" e acesse a aba "API".
- Certifique-se de que você tenha acesso como administrador da empresa.
- Copie o código do token fornecido e insira-o no valor do parâmetro que você criou para o token no Power BI.
- Para obter a URL da sua empresa, copie o trecho semelhante ao exemplo a seguir: https://suaempresa.pipedrive.com. Insira essa URL como valor no parâmetro criado para a URL no Power BI.
- 
### Conferindo a Documentação da API do Pipedrive:
Conferindo a Documentação da API do Pipedrive:
Antes de prosseguir para a etapa de obtenção dos dados da API, é recomendado consultar a documentação oficial da API do Pipedrive. Isso permitirá que você tenha uma compreensão mais abrangente dos endpoints disponíveis, bem como os dados que podem ser extraídos de cada um deles. Além disso, a documentação fornecerá informações sobre as especificações das consultas (queries) que podem ser inseridas no seu script. Veja as etapas a seguir:

Acesse a documentação oficial da API do Pipedrive e familiarize-se com os endpoints disponíveis.
Verifique os detalhes do endpoint "Deals" (negócios) para compreender as especificações das consultas e a resposta esperada.
Essas etapas iniciais são cruciais para estabelecer a base da integração entre o Power Query e a API do Pipedrive. Uma vez que você tenha configurado corretamente os parâmetros e obtido o token e a URL do Pipedrive, estará pronto para prosseguir para as próximas etapas da documentação.

## Endpoints
Na integração entre o Power Query e a API do Pipedrive, é fundamental entender o conceito de endpoints. Os endpoints são pontos de acesso na API que fornecem diferentes conjuntos de dados ou funcionalidades específicas. Cada endpoint permite interagir com determinados recursos do Pipedrive, como negócios, organizações, pessoas, atividades, entre outros.

Neste projeto, selecionaremos dois endpoints específicos: "Deals" e "Organizations". Essa seleção é baseada na relevância das informações que esses endpoints fornecem para o objetivo do projeto, mas é importante ressaltar que cabe ao usuário decidir quais endpoints são mais importantes de acordo com suas necessidades específicas.
### Endpoint "Deals":
Os "Deals" representam vendas em andamento, perdidas ou concluídas para uma organização ou pessoa. Cada negócio possui um valor monetário e deve ser colocado em uma etapa específica. Os negócios podem ser de propriedade de um usuário e seguidos por um ou vários usuários. Cada negócio consiste em campos de dados padrão, mas também pode conter vários campos personalizados. Os campos personalizados podem ser identificados por longas sequências de caracteres (hashes) como chaves. Esses hashes podem ser mapeados para DealField.key. O rótulo correspondente para cada campo personalizado pode ser obtido em DealField.name.

### Endpoint "Organizations":
As "Organizations" são empresas e outros tipos de organizações com as quais você realiza negócios. Pessoas podem ser associadas a organizações, de modo que cada organização possa conter uma ou várias pessoas.

## Script em Linguagem M
Acesse o Power BI e clique no botão "Nova Fonte" para começar a criar seu script.
- Selecione a opção "Consulta Nula" para iniciar a construção do script.
- Clique no botão "Editor Avançado" para acessar o editor de script e começar a trabalhar nele.
- Vamos simular uma requisição GET para o endpoint "Deals" da API.
- O endpoint "Deals" fornece todas as informações relacionadas à entidade "Negócios" no Pipedrive.
- Essas informações serão inseridas dentro do Pipedrive e podem ser acessadas por meio dessa requisição.
- Ao criar o script, você terá a capacidade de extrair e manipular esses dados para análises e visualizações no Power BI.
Com essas etapas, você estará pronto para começar a construir seu script no Power BI e explorar os dados do Pipedrive por meio da API.

Vamos começar inserindo a função Json.Document. Essa função retorna o conteúdo de um documento JSON, que é o formato que a API nos entrega a informação. Em seguida, vamos chamar a função Web.Contents. Ela retorna o conteúdo da URL do Pipedrive que vamos inserir.

Posteriormente, criamos a URL concatenando o Parâmetro da URL que criamos com o bloco "/api/v1/deals?api_token=" e o Parâmetro Token do Pipedrive que também foi criado.

Dentro da Query, personalizamos o api_token, usando o Parâmetro Token, definindo o limite igual a 1 (itens mostrados por página), start igual a 0 (o ponto inicial da paginação) e get_summary igual a 1 (se queremos mostrar o sumário da chamada). Todos os parâmetros da Query podem ser conferidos na documentação da API, no Endpoint de Deals.

Depois, acessamos o sumário, pegando o valor da segunda coluna (item Value). Isso nos traz o registro do total de negócios naquele Endpoint (total_count). Esse registro será usado para criar a paginação, considerando que o Pipedrive limita uma requisição a 500 registros por página.

Com o total de registros, criamos uma lista de paginação usando a função List.Generate. Essa função gera uma lista incrementando 500 registros até atingir o total de registros coletados anteriormente. Em seguida, convertemos essa lista em uma tabela usando a função Table.FromList. Para garantir a correta leitura desse dado pela API do Pipedrive, transformamos a coluna de paginação para o formato de texto usando a função Table.TransformColumnTypes.

Em seguida, adicionamos todos os dados paginados com a função Table.AddColumn. Agora, o parâmetro start será a coluna que criamos para a paginação, e o limite será de 500 registros.

Pronto, agora temos uma tabela com todos os registros de negócios paginados. Para visualizar os dados de forma tabular, basta expandir essa tabela. Lembre-se de desmarcar a opção "Use o nome da coluna original como prefixo" para evitar nomes de colunas muito longos.



## Referências 
https://www.linkedin.com/pulse/conectando-o-pipedrive-ao-power-bi-rodolfo-matte%3FtrackingId=QhvJdrtiS9yyzZxeKx6oJA%253D%253D/?trackingId=QhvJdrtiS9yyzZxeKx6oJA%3D%3D
