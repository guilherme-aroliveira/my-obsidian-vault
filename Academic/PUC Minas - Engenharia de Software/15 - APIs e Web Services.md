## **Unidade 1 - Introdução à APIs e Web APIs**
collapsed:: true
	- API --> Interface de Programação de Aplicação
	- A API permite que diferente softwares e sistemas comuniquem emtre si.
	- API Gateways fornecem funções como seguranca, roteamento, cachae e auditoria, etc...
	- Potocolo HTTP
	  collapsed:: true
		- protocolo da camada de aplicação para sistemas distríbuidos e colaborativos no formato de hipertexto.
		- a comunicação (requisição) sempre é iniciada pelo cliente
		- internet é a camada de rede que esta por baixo da web
		- web é uma aplicação em cima da internet
		- atua na camada de aplicação da pilha TCP/IP
		- a comunicação utilizada conexões TP (e UDP no caso do HTTP v3.0)
		- não guarda estado do cliente (stateless)
		- o protocolo http define um paradigma de requisição e resposta
		  collapsed:: true
			- metodo -- POST ou GET
			- recurso --> app/processamento
			- versào HTTP --> HTTP/1.1
			- linhas do cabeçalho --> campo cabeçalho e valor
			- corpo da entidade --> é o que cliente esta enviando para o servidor (payload)
		- A resposta possui versao HTTP, code status e msg status
		- códigos de retorno - Exemplos
		- metodos (verbs) http --> GET, POST ...
		  collapsed:: true
			- query string --> maneira de requisições via GET enviar parametros para o servidor, ficam visíveis na URL.
			- POST --> não é criptografado
				- usado em conjunto com formulários html
				- os dados são enviados no corpo da entidade (Requisição)
				- na Resposta apenas os headers são recebidos
				- HEAD --> serve para verificar coisas de um recurso que esta no servidor
				- Etag --> indica um hash de um documento
			- PUT --> tem a semantica de update
			- TRACE --> tem objetivo de fazer um teste
			- OPTIONS --> verifica com o servidor as opções, permite as opcoes GET, HEAD, POST, OPTIONS e TRACE.
			  collapsed:: true
				- muito utilizado para uma requisição de cors --> quando o navegador recebe uma serie de recursos de um servidor A, e o navegador pode disparar uma requisiçao para um servidor B. Por segurança, o navegador faz uma verificação para identificar se esse servidor B esta prepararo para receber requsiçoes de recursos que vieram de um servidor A ou de outros servidores. Esse tipo de chamada pode ser bloqueada.
			- CONNECT --> usado pelo navegsdor para fazer negociação do protocolo TLS.
		- A versão mais utilizada foi a 1.1 que saiu em 1999.
		- As alterações a partir de 2009, buscam tornar o HTTP um protocolo para transferencias de aplicações e dados de todos os tipos.
		- Cabeçalhos (headers)
			- São utilizados em requisições e em respostas.
			- complementam a mensagem que esta passando de um lado para o outro
			- content-type --> discreve qual que é o tipo do documento que esta sendo transitado
				- boa parte dos contetn types existentes conseguem entender o que esta sendo enviado e não é necessário enviar o content-type no header. Se o content-type for passado será feito um overload.
			- content-length --> informa quantos bytes o documento possui.
- ## **Unidade 2 - Web APIs**
  collapsed:: true
	- Abordagens de Comuicação em APIs: APIs baseada em Requisição/Respots e APIs orientada a eventos (event driven)
	- Estilos arquiteturais de APIs:
		- SOAP --> simple Object Access protocol
		  collapsed:: true
			- protocolo de troca de dados baedos em XML para envioa e recebibemto de mensagens na Internet. O SOAP define um envelopte (SOAP Envelope) para as mensagens, que possui um cabeçalho (SOAP Header) e um corpo (SOAP Body).
			- É independemente de plataforma ou linguagem de programação. O formato XML é passivel de ser trabalho em qualuqer plataforma.
			- Arquitetura
			- Estrutura de Mensagem --> baesado em XML
				- Envelope defini o inicio e o final da mensagem. É obrigatorio.
				- Header --> traz atributos opcionais da mensagem utilizada para o seu processamento. É opcional
				- Body --> Possui o conteudo da mensagem em formato XML. É obrigatório. Possui os detalhes efetivos da requsiação realizada e a menssagem onde se recebe a resposta da informação soliticada.
				- A mensagem é trocada no corpo de uma requisição e no corpo de uma respota.
			- XML --> linguagem de marcação para descrição de dados
			- WSDL --> descritor de serviços baseado em XML; descreve todas as caracteristicas, funcionalidades que um determinado serviço possui.
				- é um linguagem de descrição de um web service baseado em XML.
				- Possui os objetos: tipos de dados, padrão de mensagens, bidings, serviços e interface.
				- <message name="getTermRequest"> --> É um formato de requisição.
				- O serviço é definido com um operação <operation name="getTerm"> que possui um entrada <input message="getTermRequest"> e uma saída <output message="getTermResponse">
				- É possivel sistematizar toda a interação por meio de web-services SOAP.
				- soluções BPMS --> são suites de gerencimaneto de processos de negocio, conseguem fornecer uma plataforma para desenhos de processos, onde a esses processos é possivel associar operações, e também é possivel automatizar por meio do desenho de um fluxo e automitzar a execução e um sistema.
			- UDDI - serviço para registro e descoberta de serviços. Funciona como um catalago, que permite registrar todos os serviços disponiveis. É possivel fazer uma consulta ao UDDI que fornece um arquivo (documento) WSDL.
				- UDDI --> Universal Description and Discovery interface
				- serviço de diretório que mantem referenceia para os Web services registrados
				- reune infomações como: nomes, endereços, e numeros de telefones dos fornecedores de serviços; serviçoos oferecidos por cada fornecedor; informações tecnicas sobre a interface de cada um.
				- --> um servidor possui uma API que acessa um serviço de pagamentos, solicita ao UDDI uma consulta para descrever todos os serviços disponiveis, a requsição de mais informaçõa ao UDDI sobre esse serviço fornece um arquivo WSDL. Ao receber o WSDL é possivel montar uma consulta/requisição para o serviço de pagamentos.
				- O catalago no UDDI pode ser consultado por meio de uma requisição SOAP, a resposta também é baseado no SOAP. Todas as requisições e respostas obedecem o formato XML.
				- Poe meio de um BPMS é possivel fazer uma consulta a um UDDI e receber a relação de serviços, de forma que se consegue desenhar um fluxo e nesse fluxo é possivel atrelar determinadas operações um serviço que esta dispnivel na organização.
			- SOA --> service oritented architecture
				- Estilo de arquitetura de software cujo princio fndamental esta baseado em funcionalidade implementadas por aplicação e disponibilizadas na forma de serviços.
				- a arquiterua orientada a serviço define uma plataforma a partir da qual é possivel implementar aplicações através de serviços distribuídos.
				- Possui as camadas: consumer interface, business processes, services, service components, operational systems.
			- proposta robusta para a construção de APIs, que mescla complexidade e potência. Utiliza XML para definir comunicações estrtuturadas e se baseia em um par de cliente e servidor SOAP. Exemplo: serviços de pagamento online.
			- estabelece a maneira como se derscreve a mensagem de requisição e a mensagem de reposta; SOAP também referencia um conjunto de tecnolgoias que descrevem as apis que usam o padrão SOAP.
			- Componentes: XML, WSDL, UDDI.
			- Vantagens: comunicação estrutura e rica em recuros, intgração com sistemas corporativos.
		- REST --> Respresentational State Transfer (Tranferencia de Estado Representacional)
		  collapsed:: true
			- estilo arquitural para construção de serviços web se baseia na tranferencia de estado de representções de recursos.
			- recurso --> quaulquer informaçõe que pode ser obtida de um sistema. Exemplos: produtos, usuários, postagens, fotos.
			- estado de um recurtso --> situação a que um recursoesta, pode-se ter a representação desse estado. Exemplo: representação em arquivo JSON, representação em imagens, em texto, etc...
			- O termo RESTful caracteriza serviços Web que seguem integralmente as recomendações REST.
			- foi criado a partir de um tese de doutorado de um fucionário da Google.
			- RESTlike --> serviços implementam parcialmente as recomendações REST
			- Exemplo. APIs de mídia social.
		- GraphQL --> Graph Query Language
		- gRPC
		  collapsed:: true
			- criado pelo Google, sands for Golang.
			- remote procedural Call --> chamada a uma função qualquer, que pode ou não estar dentro do mesmo processo.
		- WebSocket
		  collapsed:: true
			- protocolo aberto que permite comuniação em duas vias entre cliente e servidos
			- tipo de API utilizado nas situações onde não há necesseriamente a requisicação e respsota, é um api baseada em eventos.
			- polling --> situação em que o cliente fica fazendo requisições ao servidor para receber as atualizações.
			- Um socket é criado a partir de um upgrade de protocolo para o servidor que irá conversar com um socket no cliente.
			- socket --> mecanismo que fica conectado no servidor e na rede.
			- socket.io --> interface para criação de websockets no node
				- usa as definições do padrão websocket, mas não é compatível com o websocket
				- arquitetura orientada a eventos
			- Caracteristicas:
				- conexao persistente entre cliente e servidor
				- permite envio de mensagens a partir do servidor de maneira independente
			- Casos de uso: sistemas em tempo real, trasmissao de jogos em sites, edição colaborativa, jogos multiplayer, aplicações de chat
		- Webhooks
		  collapsed:: true
			- também chamados de callbacks HTTP (chamada de retorno), são um tipo de API, baseado em  eventos, que permite o envio de notificações entre aplicações.
			- webhooks são chamadas que uma aplicação entrega para outra aplicação em função de algum evento.
			- possibilitam a entrega de informação de maneira assincrona.
			- Caracteristicas:
				- Disparados a partir de eventos específicos
				- acessiveis via URL diponivel publicamente (endpoints)
				- normalmente impletentado via HTTP Post com payload JSON
			- GiHub é um exemplo de empresa que utiliza Webhooks
	- formatos utilizados em APIs: XML, JSON, YAML, CSV, PrototoBuf, BSON, MessagePack
	- Mime (multipurpose Internet Mail Extensions) --> mercanismo que permite cliente e servidores, especificarem o tipo de documento transmitido durante a comunicação entre aplicações; padrao utilizado
	  collapsed:: true
		- multiplos documentos podem ser enviados de uma unica vez.
		- um tipo é dividio em duas partrs tipo/subtido e pode ter parametros opciaonis (charset, boundary)
		- Exemplos: Image/jpb --> os valores expressos no cabeçalho content-Type seguem o padrão MIME
	- Padroes de docs: WSDL - Web services Description Language --> linguagem que decreve aqueilo que esta sendo colocado no padrao SOAP; ONAPI, Swagger; API CLueprint, RAML, WADL --> Rest. Exite uma convergencia em trono do padrao OpenAPI.
	- OpenAPI specification --> utilizado para desenhar a API e apresentar os recursos disponiveis
	- API First --> estretegia que visa a criação da API antes do desenvolvimento do sistema
	- JSON --> Javascript object notation -- formato de representação de dados
	  collapsed:: true
		- documento json descreve um objeto --> {}
			- atributo "noticias" --> valor do atributo -- [] --> array
			- todos os atribjutos de um documento json devem possuir asplas duplas ("")
		- permite estrutura dados diversos
		- compativel com diversas plataformas
		- ```json
		  {
		    "noticias": [
		      {
		        "titulo": "Orgao do Minsitetio Público ...",
		        "resumo": "Procradors fazem investida ...",
		        "data": "18.out.2021 as 20h20",
		        "autor": "Italo Nogueira",
		        "fonte": "FOLHAJUS",
		        "texto": "O CNMP (Conselho Nacinal ...)",
		      }
		    ]
		  }
		  ```
	- API Restful
		- Retful é um padrão baseado em recursos (Resources). Exemplo: /Carros/1 --> busque dos carros o carro de ID 1
		- Resources são objetos (informações que estão no banco) --> todo REST é baseado nisso
		- Controller --> operações realizadas em cima dos recursos, mas que não se enquadram no PUT, PATCH, GET, POST, etc..
		- QParameter -->
	- ferramentas: insomnia, postman, teste automatizado.
	- alguns tipos de testes automatizados: unidade --> pose se testar o metodo GET de um item, integração --> testa unidade do Controller com outras partes como a parte de busca no banco de dados, performance, stress --> continua a execução até quebrar, busca o limite da API.
	- middlewaes são funções que são asscociadas a aplicação do express para fazer o processamento de um endpoint de um determinado tipo de requisição --> dado pelo path (Exemplo: /api/v1).
- ## **Unidade 3 - Segurança em APIs**
- ## **Unidade 4 - Gerenciamento de APIs**