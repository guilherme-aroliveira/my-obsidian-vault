## **Unidade 1 - Estilos Arquiteturais**
	- <p><span style="color:#d65d0e">Estilo arquitetural</span> <span style="color: #3588E9">--></span> é a grande forma que um arquiteto busca ao construir um objeto, ele deve realizar uma função (uma forma segue a função).</p>
	- <p><span style="color: #3588E9">--></span> Não exite um estilo arquitetural de software pior ou melhor, mas aquele mais apropropriado em um determinado contexto.</p>
	- <p>Deve-se fazer uma coleta dos condutores arquiteturais <span style="color: #3588E9">--></span> tecnica.</p>
	- <p>Um <span style="color:#d65d0e">condutor arquitetural</span> (architectural triber) é um direcionador estratégico para que se possa avançar na arquitetura. Exemplo: condutor arquitetural que esta ligado a segurança.</p>
	- Para cada tipo de problema do mundo real, iremos ter condutores mais apropriados.
	- <p>Um exercício importante que deve ser feito por um arquiteto no inicio de um projeto ou de um ciclo de melhoria de arquitetura é a <strong>coleta de condutores arquiteturais</strong>: conversando com especialistas de negocios, lendo informações do segmento. Dessa forma, é possivel elaborar um conjunto de condutores (pequenos elementos).</p>
	- Com a lista de condutores, será possivel conhecer que estilos são mais ou menos apropriados.
	- Condutores Artuiteturais Comuns: Usuabilidade, Performance, Segurança, Confiabilidade, Extensibilidade, Interopelabilidade, Manutenibilidade.
	- <p><span style="color: #3588E9">--></span> A escolha de um estilo arquitetural é dado pela <strong>coleta de condutora arquiteturais</strong> (organização de arquitetura).</p>
	- <p><strong style="color: #689d6a">Estilo Baseado em Camadas</strong>:</p>
	  collapsed:: true
		- <p>Ligado a um <strong>especto básico</strong> <span style="color: #3588E9">--></span> como evitar que o código cresça de uma forma caótica com elementos que deveriam estar separados dentro dessa organização de códigos.</p>
		- Formas de organizar as grandes camada lógicas e também representar camadas física da aplicação.
		- As camadas logicas e fisicas devem ser organizadas de acordo com a intenção da separação para facilitar a manutenção e o teste do código.
		- Em computação é muito comum que a gente tenha dois grandes modelos de consumo: aplicações que consomem muitos dados (data bound) e aplicações que terão muito consumo de cpu (CPU Bound).
		- É um estilo bastante flexível, ele fornece muitas configurações de como se pode organizar as camadas logícas e físicas.
		- <p><span style="color:#d65d0e">Camada fechada</span> <span style="color: #3588E9">--></span> expõe um conjunto de funcionalidades para a camada de nível mais acima, é utilizada como elemento de mediação. É uma regra utilizada no mercado para garantir a manutenibilidade do código.</p>
		  collapsed:: true
			- <p>Presentation Layer [Closed] --> Busniess Layer [Closed] --> Persistence Layer [Closed]--> Database Layer [Closed]</p>
		- <p>MVC, MVVM, MVP <span style="color: #3588E9">--></span> organizações conceituais de camadas lógicas.</p>
	- <p><strong style="color: #689d6a">Estilo Baseado em Pipelines</strong>:</p>
	  collapsed:: true
		- <p>Pipeline -> representa um estilo comum no mercado para que se possa montar arquiteturas escaláveis, extensiveis e com boa manutenibilidade.</p>
		- Pode ser visto dentro da area de BI --> as informações relacionais e não-relacionais são tranformadas em inteligência de negócio.
		- (Filter) --- Pipe ---> (Filter) --- Pipe ---> (Filter)
		- ETL --> Extração Tranformação Carga (Load)
		- As várias extrações são exemplos de filtros.
		- --> Quando se tem vários filtros conectados por Pipes tem-se um estilo baseado em pipelines.
		- É uma arquitetura se move da esquerda para direita, entregando informações conectadas em pipes para outros filtros.
		- É um estilo utilizado em Telecom --> são executados processos em tempo real
		- AWS Lamba --> exemplo de estilo baseado em pipelines
	- <p><strong style="color: #689d6a">Estilo Baseado em Micro-Kernel</strong>:</p>
	  collapsed:: true
		- <p><span style="color:#d65d0e">Kernel</span> <span style="color: #3588E9">--></span> representa núcleo em inglês</p>
		- Arquitetura que permite que pontos de extensiblidade sem que o núcleo precise ser modificado --> desenho/estilo arquitetural
		- Exemplos: web-broser (navegador), um plugin pose ser colado, sem afetar o producto central.
		- Nesse estilo arquitetural uma extensão/plugin pode ser adicionado, sem que hava a necessidade de recompilar o producto central. E há um mecanismo de segurança que impede que o plugin corrompa o estado da aplicação.
		- Estilo fundamental para se trabalhar com extensiblidade.
		- Exemplo de mercado: Domínio de RPs --> utilizam o conceito de micro-kernel
		- <p><span style="color:#d65d0e">O micro-kernel</span> pode ser tecnicamente parcionado. Exemplo: ( Core System  [Presentation Layer] [Business Layer] [Persistence Layer] ), também pode possuir elementos ligados ao particioamento do domínio <span style="color: #3588E9">--></span> muito utilizado em RPs.</p>
		  id:: 66364072-9ff4-4321-a989-bbb6b408854e
	- <p><strong style="color: #689d6a">Estilo Baseado em Serviços</strong>:</p>
	  collapsed:: true
		- Traz uma alternativa caso se deseja implantar coisas em ciclos curtos.
		- A aplicação é particionada logicamente, e o domínio da aplicação é formado por um conjunto de componentes (grandes componenetes) que funcionam de maneira apartada (lógica e fisicamente). É uma arquitetura distribuída, ou seja, cada componente pode estar operando em seu próprio nó.
		- Cada componenente possui a sua própria lógica de negócio, e não pussui dependências explicitas a outros componentes.
		- Pode pussuir um único bando de dados.
		- --> Microsserviço é um tipo particular de arquitetura baseada em serviços.
		- Os componentes representam os serviços da aplicação.
		- Pode se criar um malha de componentes, que pode gerar informações para várias interfaces gráficas diferentes em produtos diferentes (escala da aplicação). Exemplos: Interfaces mais monolítica; Interface que lida com questões específicas de autenticação.
		- Os dados podem ser distribuídos de diversas maneiras: em um unico banco de dados ou múltiplos banco de dados (cada componente pode manipular o seu próprio BD).
		- É uma arquitetura voltada para extensibilidade, implantabilidade facitilitada e implantação modular.
	- <p><strong style="color: #689d6a">Estilo Baseado em Evetos</strong>:</p>
	  collapsed:: true
		- Evento --> mensagem com uma marcação temporal
		- É uma arquitetura projetada especialmente para lidar com eventtos e processa-los.
		- Requisição --> eventos coletados em certos locais. Exemplo: compra em loja eletrônica.
		- Os componenentes podem processar um determinado evento, e colocar outros eventos do conjunto de malha de eventos que serão manipulados, o evento pode ser gravado em um banco de dados por exemplo.
		- Orquestrador --> maestro que organiza um grande número de eventos.
		- É uma arquitetura muito popular quando se precisa fazer processos de integração de dados.
		- --> É bastante escalável.
		- Broker --> tipo de topologia de evento. Nesa arquitetura o evento é colocado dentro um local persistente (Canal), que pode ser posteriormente retirada do Canal e processada por um componenente (lógica de negócio), sendo armazenada em um outro Canal. Ë bastante utilizada por empresas para processamento que exigem alta escalabilidade e alta tolerância a falhas.
		- Vários Processadores de Evento podem estar ouvindo um Canal, ou um Procesador pode enviar mensagens para várias Canais.
		- Na topologia Broxer, o fluxo é distribuído dentro de vários Canais, sendo que cada Canal é responśavel por uma determinada mensagem, e os Processadores pegam de uma forma distribuída para consumir ou colocar informações nos Canais. Há uma inteligência distribuída na organização dos eventos. Exemplos: pix ou compra na Amazon.
		- Mediator --> Topologia na qual há um mediador que é reponsável por fazer a manipulação de colocar as mensagens nas Filas e cordenar a entrada e saída da informação.
		- Grandes processos bancários como Doc, Ted e Pix são baseados no Estilo Baseado em Eventos.
		- É um estilo bastante utilizado em arquiteturas de núvem.
	- <p><strong style="color: #689d6a">Estilo Baseado em Espaços</strong>:</p>
	  collapsed:: true
		- São arquiteturas onde a computação é distribuída em múltiplos nós.
		- --> Se tornou mais popular por causa da infraestrutura de núvem.
		- A ideia básica é que se tenha um conjunto de nós de computação (VMs, Docker, malhas de Kubernetes) e um banco de dados distríduido, mas que a aplicação irá enxergar apenas um único banco de dados.
		- Arquitetura bastante útil quando se deseja realizar operações em larga escala, ou seja, há um grande número de máquinas que estão relizando processamentos através de uma grande mémoria compartilhada. Exemplo: ChatGPT.
		- Exemplos de ferramentas gratuitas: Docker, Kubernetes, Kafka, Apache Cassandra.
	- <p><strong style="color: #689d6a">Estilo Baseado em Orquestração de Serviços</strong>:</p>
	  collapsed:: true
		- Estilo que se tornou bastante popular com os barramentos de serviços (SB).
		- Há um conjunto de Serviços de negócio que irão conectar a interfaces diversas e que irão enviar eventos para uma peça arquitetural, que irá operar como um hub (elemento de orquestração).
		- O papel do SB é fazer uma conexão do serviço de negócio com os serviços mais baixo nível dentro da malha.
		- Os serviços de mais baixo nível irão se comunicar ao serviços da aplicação, de infraestrutura, e os dados serão orquestrados da esquerda para direita.
		- --> O controle de tolerança a falhas, controle de estados, segurança, monitamento e auditoria, são gerenciados pelo barramento de serviços. 
		  > Nota: Um dos motivos que levaram ao surgimento dos microsserviços, foram as falhas na tentativa de acionar em larga escala arquitetura de SB.
	- <p><strong style="color: #689d6a">Estilo Baseado em Microsserviços</strong>:</p>
	  collapsed:: true
		- Nesse estilo há um conjunto de microsserviços que irão separar os elementos de dominio da aplicação, com uma separação lógica e física.
		- Um serviço representa um componente de negócio independente.
		- É comum que em microsserviços haja pequenas máquinas (containeres) que permitem rodar um conjunto de microsserviços sem trazer muito ônus ao sistem operacional.
		- Um serviço terá de forma mandatoria um banco de dados lógico (proteção modular) dedicado.
		- Caso um serviço deseja comunicar com outro serviço, ele pode enviar um mensagem que é colacada em uma Fila (Canal), sendo processada e criando um desacoplamento entre os microsserviços.
		- Microsserviço combina uma arquitetura beseada em serviços e uma arquitetura beseada em eventos.
		- A camada de API é criada, para isolar o mundo do backend (mundo militarizado que operam em redes privativas) do mundo desmilitarizado de aplicativos móveis ou aplicativos web tradicionais.
		- Chassi --> padrão arquitetural dentro de microsserviço, utilizado para isolar um serviço do outro.
		- É possivel que haja Fron-End Monolítico, que irá chamar um conjunto de APIs para se comunicar a um determinado serviço da malha de microsserviços.
		- Também é possivel que haja Micro-Front Ends, forma mais moderna de projetar arquiteturas de Fron-End.
		- --> A arquitetura de Microsserviço é utilizada, quando o objetivo é obter uma capacidade de colocar produtos em produção com muito mais velocidade (implantabilidade).
- ## **Unidade 2 - Estilo em Camadas**
  collapsed:: true
	- <p><strong style="color: #689d6a">Padrão MVC</strong>:</p>
	  collapsed:: true
		- Surgiu como conceito para separar o código de Front-End do código de Back-End.
		- Tem como propósito separar a camada de redenrização de apresentação de dados para os usuários finais das camadas da inteligência de negócio orgnizada pelo Model.
		- Movel - View - Controller
		- A requisição inicia do Controller que realiza regras de mediação - emite um comando contra o Model.
		- O Controller tem uma informação específica para a plataforma onde será renderizada.
		- O Model contêm as regras que permitem a manipulação dos dados da aplicação de negócio que manter a aplicação.
		- --> O Model é agnostico de tecnologia, não há uma ligação com tecnologia de visualização.
		- O View recebe os dados do Controller.
		- Ordem de chamadas no MVC
		  collapsed:: true
			- 1.
				- Usuário (tela) invoca algum Controller
				- Controller valida requisição e seleciona o Model a ser chamado
			- 2.
				- Model executa regras de negócio, prepara e retorna para o Controller
			- 3.
				- Controller entrega dados para View através de uma projeção do Model
				- View desenha os dados para os clientes da aplicação
		- --> A organização de chamada a dados esta fora do escopo do MVC. Normalmente o MVC tem que estar acoplado com outros padrões, como por exemplo o DDD.
		- Ao implementar o MVC na web:
			- O Model e Controller operam no Back-End.
			- Toda a comunicação entre View e Controller irá envolver uma chamada de rede.
			- O MVC irá privilegiar a organização de logica de mediação da camada de Back-End --> ocasiona um peso maior no servidor.
		- Um arquitetura baseada em MVC busca separar em pastas/packages de forma que models, views, e controllers estejam apartados.
	- <p><strong style="color: #689d6a">Padrão MVVM</strong>:</p>
	  collapsed:: true
		- Surgiu nos anos 90 devido a evolução das interfaces gráficas, sendo bastante utilizado em interfaces Desktop, como por exemplo o Microsoft Windows.
		- Foi popularizado pelo Angular - que permitiu facilitar interfaces mais modernas.
		- <p>Arquiteturas MVVM foram <strong style="color: #b16286">desenhadas para aplicações web mais modernas</strong>, onde há um grande volume de interações.</p>
		- <p><span style="color:#98971a">Model</span> - <span style="color:#98971a">View</span> - <span style="color:#98971a">ViewModel</span></p>
		- <p>O <span style="color:#98971a">Model</span> opera da mesma forma que no MVC <span style="color: #3588E9">--></span> posssui um modelo de dominio bem formado, não possui objetos anêmicos.</p>
		- <p>O <span style="color:#98971a">ViewModel</span> possui um papel arquitetural equivalente ao <span style="color:#98971a">Controller</span>, mas com algumas diferenças. O ViewModel irá operar junto a View, em uma arquitetura Web irá operar dentro do navegador em um código JavaScript. O ViewModel reside no mesmo lado do cliente e terá um cash dos dados.</p>
		- <p><span style="color: #d65d0e">delegação</span> <span style="color: #3588E9">--></span> padrão de como a operação é relizada (chamada ao Model através de uma API).</p>
		- <p>O <span style="color:#98971a">View</span> continua com a mesma função arquitetrual de desenhar os elementos - mas fara toda a comunicação com as interfaces gráficas, a requisição não vai para um Controller como acontece no MVC.</p>
		- O View irá fazer um consulta dos dados no ViewModel. A ViewModel representa um cash para o View, pois muitas vezes os dados estarão locais. Caso a informação não esteja localmente, há uma chamada de rede para o Model que irá retornar uma reposta para o ViewModel.
		- O View terá delegações com o ViewModel, para desenhar a informação.
		- <p><span style="color: #d65d0e">Objetos anêmicos</span> <span style="color: #3588E9">--></span> classe que possui apenas atributos, getters e setters.</p>
		- <p><span style="color: #d65d0e">Modelo de Domínio Anêmico</span> é <strong style="color: #b16286">anti-padrão arquitetural</strong>.</p>
		- No MVVM as comunicações entre View e ViewModel ocorrem localmente, tipicamente escritas em JavaScripts armazenadas no navegador.
		- <p><span style="color: #3588E9">--></span> Há uma chamada bem menor de chamadas de rede.</p>
	- <p><strong style="color: #689d6a">Padrão DDD</strong>:</p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">Desenho Dirigido por Domínios (DDD)</span> <span style="color: #3588E9">--></span> abordagem para o desenvolvimento de software que enfativa a importância do domínio central e da lógica do domínio. É uma ferramenta de comunicação manifestada no código.</p>
		- Surge para resolver os problemas de comunicação a partir de uma perspectiva tecnica, entre times de negócio e times de desenvolvimento.
		- <p>Envolve a criação de astrações de software chamada <strong style="color: #b16286">modelos de dominio</strong> que encapsulam lógicas de negócios complexa e vinculam as condições reais do aplicativo de um produto de código.</p>
		- <p>Facilita a organização de grandes dominios em dominios menores chamados de contextos limitados <span style="color: #3588E9">--></span> um grande produto é distribudo em componenetes autonomos, chamados de microsserviços.</p>
		- <p><span style="color: #3588E9">--></span> Cria um sistema com uso pleno da orientação a objetos.</p>
		- <p><span style="color: #d65d0e">Linguagem ubíqua</span> <span style="color: #3588E9">--></span> uma linguagem comum e compartilhada entre todas as pessoas envolvidas no desenvolvimento do software. É uma linguagem composta por terminologia de negócio - manifestada no códgio fonte.</p>
		- <strong style="color: #d79921">Camadas dos DDD</strong>
		  collapsed:: true
			- <p>1. <span style="color:#98971a">Dominio</span>: camada mais importante, na qual terá as classes com atributos e comportamentos, as classes com relações e toda a inteligência de negócio. Porém não tem uma visão orientada a funcionalidade.</p>
			- <p>2. <span style="color:#98971a">Infraestrutura</span>: camada que contêm os elementos de natureza tecnologica. Organiza os repositórios com a lógica específica de persistência de dados. A Infraestrutua conheça o Domínio, mas o Dominio desconhece a Infraestrutua --> Ignorância da Infraestrutua (padrão de desenho do DDD).</p>
			- <p>3. <span style="color:#98971a">Serviço</span>: fornece uma visão dos serviçís da aplicação. Ela utiliza o Dominio e Infraestrutua, para fazer uma regra de coordenação, fornecendo para a camada de Aplicação o serviço completo. Exemplo: cadastrar uma nova conta.</p>
			- <p>4. <span style="color:#98971a">Aplicação</span>: responsável pelo projeto principal. Aqui serão implementados os controladores e a exposição de APIs. Tem a função dereceber todas as requisições de direcioná-las a algum Serviço para executar uma determinada ação.</p>
		- <p><span style="color: #3588E9">--></span> É um padrão puramente para o backend.</p>
		- Estrutura simplicada de pastas
		  ```bash
		  |---- application
		  |     |---- services
		  |
		  |---- domain
		  |     |---- entities
		  |     |---- repositories
		  |     |---- value-objects
		  |
		  |---- infrastructure
		  |     |---- repositories
		  |     
		  |---- interfaces
		        |---- controllers
		  ```
		- O Domínio no DDD possui a parte mais importante que esta cuidando dos conceitos e regras de negócio, da manisfetação da linguagem ubíqua.
		- O DDD possui uma <strong style="color: #b16286">hierarquia de objetos conceituais</strong>: <span style="color:#98971a">entidades</span> - <span style="color:#98971a">raízes agregadas</span> - <span style="color:#98971a">objetos de valor</span>. Entidades representam o dominio da aplicação.
		- <p><span style="color: #d65d0e">Contrato de repositórios</span> <span style="color: #3588E9">--></span> estabalece que operações que um repositório de uma conta deveria fornecer. O repositório é apenas um contrato. A implementação do repositório não fica dentro do Domínio --> apenas possui uma pura lógica de negócio.</p>
		- <p>A <span style="color: #d65d0e">camada de Serviço</span> irá conter uma fachada para manipular os coceitos da aplicação. Não há regras de negócio apenas de mediação. O serviço possui acesso a cada de repositório (Infraestrutura) e também possui acesso a cadama de Domínio.</p>
		- <p><span style="color: #3588E9">--></span> No padrão DDD o componente responsável por fornecer acesso e persistência aos <span style="color: #d65d0e">Aggregates</span> é o <span style="color: #d65d0e">Repositório</span></p>
		- A infraestruta pode ter diversas implementações de um contrato, de acordo com a camada real de persistência, como por exemplo, uma implementação para MySQL e uma implelentação para MongoDB.
		- <p><span style="color: #3588E9">--></span> No DDD se irá ter regras em vários níveis, regras no nível do value obejct, regras no nível de uma entidade, regras no nível de uma raiz agregada e até regras no nível de serviço (regras que irão cuidar de uma orquestração).</p>
		- Livro Design Patterns
	- <p><strong style="color: #689d6a">Padrão Arquitetura Limpa</strong>:</p>
	  collapsed:: true
		- Padrão que se tornou mais popular a partir do lançamento do livro Clean Architecture de Robert Martin.
		- <p>É um conjunto de conceitos e príncipios que <strong style="color: #b16286">visam a construção de sistema com alta coexão</strong>, baixo acoplamento e separação de responsabilidades.</p>
		- Foi baseada em melhores prática de design de software (Design Patterns).
		- <p><span style="color: #d65d0e">SOLID</span> <span style="color: #3588E9">--></span> conjunto de principios que ajudam o produto a ser mais extensível.</p>
		- <p><span style="color: #d65d0e">inversão de dependencias</span> <span style="color: #3588E9">--></span> mecanismos de descacoplamento de código</p>
		- <p><span style="color: #3588E9">--></span> SOLID e inversão de dependencias sõa principios orientadores da arquitetura limpa</p>
		- <p>A regra principal é a <span style="color: #d65d0e">Regra de Depedência</span> <span style="color: #3588E9">--></span> das depedências são de fora para dentro, as camadas mais internas não devem depender das camadas mais externas. As regras de negocio estarao no nucleo e não possuem nenhum dependencia para o mund oexterno.</p>
		  collapsed:: true
			- As camadas mais internas representam regras de negocio de aplicação e regras de neogico mas corporatvo.
			- As cadas externas irao representar aspectos mais volateis, mais tecnologicos.
			- A camada vermelha (Enterprise Business rules) não conhece a camada amarela (Application business rules).
		- A arquitetura limpa busca garantir que detalhes tecnologicos não afetem as regras de negocio (separaçaoo das preocupacoes).
		- <p><span style="color: #d65d0e">Principio do Reuso</span> <span style="color: #3588E9">--></span> nao se deve entregar para o usuario mais do que o necessário.</p>
		- <p><span style="color: #d65d0e">Papel do arquiteto</span> <span style="color: #3588E9">--></span> ennxergar os pontos de mudanca e criar limites para separar as partes do sistemas de forma coesa.</p>
		- <p><span style="color: #d65d0e">Divisão em camadas</span> <span style="color: #3588E9">--></span> mecanismo primário</p>
		- <p><strong style="color: #d79921">Ordens das camadas de uma Arquitetura limpa:</strong> 1. Framework & drivers (camada azul), 2. Interface adapters (camada verde), 3. Application Business rules (camada amarela), 4. Enterprise business rules (vermelha)</p>
		  collapsed:: true
			- <p>Camada azul <span style="color: #3588E9">--></span> responsável por todo detalhe tecnologico</p>
			- <p>Camada verde <span style="color: #3588E9">--></span> tradução dos dados de negócio para dados da camada tecnologica</p>
		- <p><strong style="color: #d79921">Estrutura de pastas:</strong></p>
		  collapsed:: true
			- <p>Pacote Casos de Uso (usecases) <span style="color: #3588E9">--></span> manipula o domain e infrastructure</p>
			- Pacote de Domínno (domain)
			- Pacote de Infraestrutura (infrastructure)
		- É uma arquitetura que faz mais sentido em um sistema maior, carrega pre requisitos ligados a Orientaco a Objetos e padrao de desenho e implementação.
		- <p><span style="color: #3588E9">--></span> O objetivo da arquitetura limpa é na organização do código para criar um sistema escalável. Enquanto o DDD, foca na modelagem de dominio. Ambos possues objetivos complementares.</p>
- ## **Unidade 3 - APIs**
  collapsed:: true
	- <p><span style="color: #d65d0e">API</span> <span style="color: #3588E9">--></span> <strong style="color: #b16286">Interface de Programação de Aplicação</strong></p>
	- Uma API é uma interface que uma aplicação de software apresenta a outras aplicações. São blocos de contstrução que permitem a interoperabilidade para as principais plataformas de negócios na web.
	- <p><span style="color: #d65d0e">Estilo Arquitetural de APIs</span> <span style="color: #3588E9">--></span> estilo onde uma API é construída.</p>
	- APIs simplificam o uso de outros softwares.
	- Uma API de forma forma, esta encapsulando e expondo um contrato de um backend (informação de um banco de dados), e essa API pode servir a mecanismos diferentes.
	- <p><span style="color: #d65d0e">GRPC (Google RPC)</span> <span style="color: #3588E9">--></span> Protocolo que consegue trabalhar sobre HTTP2 e encapsular os dados binariamente.</p>
	- <p><span style="color: #d65d0e">Proto Buffer</span> <span style="color: #3588E9">--></span> protocolo de dados</p>
	- As soluções em nuvem SaaS normalmente consistem em um aplicativo da Web e APIs (Exemplo: Dropbox, que opera sobre o S3 da AWS).
	- APIs fornecem or recursos, que são essenciais para conectar, estender e integrar software.
	- <p><span style="color: #d65d0e">Testabilidade de APIs</span> <span style="color: #3588E9">--></span> teste de contrato.</p>
	- Toda API deveria ter um teste automatizado que verifica aquela API.
	- <p><strong style="color: #d79921">API Platform</strong><ul style="list-style-type:disc"><li><span style="color:#98971a">API Development Platform</span> <span style="color: #3588E9">--></span> plataforma para desenhar, testar e implanter um API</li><li><span style="color:#98971a">API Runtime Platform</span> <span style="color: #3588E9">--></span> plataforma que sustenta uma API em um ambiente de produção (exemplo: Gateways de API)</li><li><span style="color:#98971a">API Engagement Platform</span> <span style="color: #3588E9">--></span> portais gerar documentação</li></ul></p>
	- <p><strong style="color: #d79921">Ciclos de vida de APIs</strong>: <strong style="color: #b16286">Develop</strong> <span style="color: #3588E9">---></span> <strong style="color: #b16286">Deploy</strong> <span style="color: #3588E9">---></span> <strong style="color: #b16286">Publish</strong></p>
	- <p><span style="color: #d65d0e">API first</span> <span style="color: #3588E9">--></span> processo para descrever uma API em um padrão (exemplo: Open API), que habilita pessoas de Front-End e Back-End.</p>
	- <p><span style="color:#98971a">Postman</span> <span style="color: #3588E9">--></span> ferramenta para testes de APIs, permite emular e simular contratos.</p>
	- <p><span style="color:#98971a">OAth0</span> <span style="color: #3588E9">--></span> API para serviço de autenticação.</p>
	- <p><span style="color: #3588E9">--></span> Plataforma de execuação hospeda uma API.</p>
	- Plataforma de Engajamento permitem criar portais especializados em APIs, que permitem assim, guiar o desenvolvedor para o uso e teste de uma API.
	- <p><span style="color: #3588E9">--></span> Livro API Architecture</p>
	- <p><span style="color: #d65d0e">Legado</span> <span style="color: #3588E9">--></span> aquilo que esta em produção.</p>
	- <p><strong style="color: #d79921">Táticas de APIs</strong> <span style="color: #3588E9">--></span> mecanismo pragmáticos para a construção e consumo de APIs.<ul style="list-style-type:disc"><li><span style="color:#98971a">REST/HTTP</span> <span style="color: #3588E9">--></span> abordagem padronizda para expor recursos na Web</li><li><span style="color:#98971a">RPC/gRPC</span> <span style="color: #3588E9">--></span> utilização e construção de APIs centradas em verbos e/ou a utilização de mecanismo mais performáticos, que irão utilizar protocolos mais eficientes de traporste e protocolos mais compactos para a serialização dos dados entre to cliente, servidor e servidor-cliente</li><li><span style="color:#98971a">WebSocker</span> <span style="color: #3588E9">--></span> abordagem que facilita a comunicação bidirecional entre o cliente e servidor</li><li><span style="color:#98971a">GraphQL</span> <span style="color: #3588E9">--></span> linguagem de consulta de APIs</li></ul></p>
	- <p><strong style="color: #689d6a">REST</strong></p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">REST</span> <span style="color: #3588E9">--></span> Tranferencia de Estado Representacional</p>
		- Nasceu a partir da diseminação do HTTP, e pode ser definido como uma abordagem para que se possa transferir estado representacional entre servidores.
		- É a escolha mais popular para o desenvolvimento de API.
		- Em teoria é possivel implementar um arquitetura REST utilizando qualquer tipo de protocolo, mas na prática de mercado é mais comum tutiliz-alo com HTTP e HTTPS.
		- REST é baseado no conceito central de resursos.
		- <p>Um <span style="color: #d65d0e">recurso</span> é uma <strong style="color: #b16286">entidade/conceito</strong> que pode ser identificada, nomeada, exposata e trabatada na web.</p>
		- Um API web baseada em REST expose dados como recusos e usam métodos HTTP padrao para representar operações/transações Criar, Ler, Atualizar e Excluir (CRUD) que podem ser feitas contra esses recursos.
		- <p><strong style="color: #d79921">Exemplo - API da Stripe</strong></p>
			- A Stripe manipula meios de pagamentos através de APIs.
			- A API representa clientes, encargos, saldados, reembolsos, eventos, arquivos e pagamentos como recursos.
			- <p><span style="color: #d65d0e">Requisição HTTP</span> para recuperar um cobranca da API Stripe:</p>
			  > <p>GET
			  /v1/charges/ch_CWyutlXs9pZyfD 
			  Host api.stripe.com
			  Authorization: Bearer
			  YNoJ1Yq64iCBhzfL9HNO00fzVrsEjtV</p>
			  
			  > <p><span style="color: #55ffff">GET</span> <span style="color: #3588E9">--></span> operação de leitura</p>
			  <p><span style="color: #55ffff">v1</span> <span style="color: #3588E9">--></span> representa a versão da API (é uma boa prática)</p>
			  <p><span style="color: #55ffff">charges</span> <span style="color: #3588E9">--></span> representa um recurso; é uma convensão colocar no plural</p>
			  a chave após o recurso representa um elemento espećifico
		- <p><strong style="color: #d79921">Regras comuns REST</strong></p>
			- <p><strong style="color: #689d6a">Uso de Métodos HTTP</strong></p>
				- <p><span style="color: #d65d0e">Métodos HTTP</span> como <span style="color:#98971a">GET</span>, <span style="color:#98971a">POST</span>, <span style="color:#98971a">UPDATE</span> e <span style="color:#98971a">DELETE</span> informam o servidor sobre a ação a ser realizada.</p>
				- Diferentes métodos HTTP invocados na mesma URL fornecem funcionalidades diferentes.
				- <p><span style="color:#98971a">POST</span> <span style="color: #3588E9">--></span> usado na maioria dos casos, para criar novos recursos</p>
				- <p><span style="color:#98971a">GET</span> <span style="color: #3588E9">--></span> usado para ler recursos. Requisições GET nunca mudam o estado do recurso. O GET é idempotente.</p>
				- <p><span style="color:#98971a">PUT</span> <span style="color: #3588E9">--></span> usado para substitui um recurso, também é idempotente</p>
				- <p><span style="color:#98971a">PATCH</span> <span style="color: #3588E9">--></span> usado para atualizações parciais para os recursos existentes.</p>
				- <p><span style="color:#98971a">DELETE</span> <span style="color: #3588E9">--></span> usado para excluir recursos existentes. Também é idempotente</p>
			- <p><strong style="color: #689d6a">Nomeclatura</strong></p>
				- <p>Os recursos fazem parte das URLs, como <span style="color: #55ffff">/usuarios</span></p>
				- <p>Para da recurso, duas URLs são geralmente implementadas: uma para a coleção, como <span style="color: #55ffff">/usuarios</span>, e uma para um elemento específico, como <span style="color: #55ffff">/usuarios/U123</span></p>
				- <p>Nomes são usados em vez de verbos para definir recursos, como <span style="color: #55ffff">/usuarios/U123</span></p>
			- <p><strong style="color: #689d6a">Códigos de Resposta</strong></p>
				- Os códgios de status de reposta HTTP padrão são desenvolvidor pelo servidor indicando sucesso ou falha.
				- Códigos na faixa 2XX indicam sucesso
				- Códigos 3XX indicam que um recurso se moveu
				- Códigos na faixa 4XX indicam um erro do lado do cliente
				- Códigos na faixa 5XX indicam erros do lado do servidor
			- <p><strong style="color: #689d6a">Formatos de resposta</strong></p>
				- <p>As APIs REST podem retornar respostas JSON (padrão) ou XML.</p>
				- <p>No Brasil, o XML é comum em APIs do governo para facilicar a governança de dados.</p>
			- <p><strong style="color: #689d6a">Operações não CRUD</strong></p>
				- <p>Há duas abordagens comumente usadas em operações não crud: <ul><li><span style="color: #55ffff">GET livros/empromocao</span> <span style="color: #3588E9">--></span> cria ação como um subrecurso</li><li><span style="color: #55ffff">GET livros?tipo=empromocao&categoria=autoajuda</span> <span style="color: #3588E9">--></span> cria uma ação através de parâmetros de entrada (query string) </li></ul></p>
	- <p><strong style="color: #689d6a">RPC e gRPC</strong></p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">RPC</span> <strong>significa</strong> em sua origem <strong style="color: #b16286">Chamada de Procedimento Remoto</strong>, é um dos paradigmas mais simples de API, em que um cliente executa um bloco de código em outro servidor.</p>
		- <p><span style="color: #3588E9">--></span> Toda chamada a um procedimento remoto, uma forma de RPC esta sendo utilizada. Genericamente, toda comunicação remota é uma tipo de RPC</p>
		- Enquanto o REST é sobre recurso, a RPC é sobre ações. Os clientes tipificam um nome e argumentos de método para um servidor e recebem de volta JSON ou XML. Tanto REST quanto RPC podem usar o protoclo que quiserem, como HTTP, HTTPS, e inclusive MQTTP.
		- <p>Há outras implementações de mercado que surgiram baseados na ideia do RPC, como o Apache Thrift e Google gRPC --> utilizam HTTP 2.0.</p> > Nota: O HTTP 2.0 consume menos recursos do servidor e irá dar maior escalabilidade para uma aplicação que demanda muita comunicação simultanea.
		- <p>Os protocolos de alto desempenho, utilizam protocolos de dados que irão gerar uma compactuação maior. As informações são compactadas e enviadas de forma binária, utilizando procotocolo como o <span style="color: #d65d0e">ProtoBuffer</span>.</p>
		- <p><span style="color: #d65d0e">gRPC</span> é uma implementação específica de RPC focada em aplicações que requerem alto desempenho. É uma API baseada em verbos.</p>
		- <p><span style="color: #3588E9">--></span> Uma <strong style="color: #b16286">API orientada a verbo</strong> normalmente vai utilizar um único metodo HTTP, tipicamente um POST, por convenção.</p> > API baseada em verbos facilitam a organização de contratos entensos. Fornecem facilidade e extensibilidade para produção de APIs.
	- <p><strong style="color: #689d6a">GraphQL</strong></p>
	  collapsed:: true
		- É uma linguagem de consulta para APIs criada pelo Facebook em 2012.
		- O GraphQL permite que os cliente definam a estrutura dos dados necessários, e o servidor retorna exatamente essa estrutura.
		- No GraphQL é possível manipular o servidor interagindo através de comandos de consultas (querys) ou em comandos de modificações (mutations).
		- <p><span style="color: #3588E9">--></span> a <span style="color: #d65d0e">query</span> é enviada ao servidor através de um endpoint único padronizado (objeto JSON), o servidor faz uma parsing do que esta sendo buscando e retorna um JSON como resposta.</p>
		- As consultas da GraphQL retornam resultados previsíveis, dando aos clientes controle sobre os dados que são devolvidos.
		- <p>O servidor define um esquema de dados com tipos aninhados. O servidor cria um código que interpreta as requisições que enviam pacotes de dados baseados no esquema de dados, e retorna ou altera as coleções de dados necessários.</p> > Dependendo de como o cliente manipula e envia o JSON de requisição, ele pode exigir um grande volume de dados a medida que esse esquema precisa ser navegado e montado. Isso pode provocar uam carga no processamento do servidor, e caso dados sejam buscados no banco de dados, pode demandar um grande volume de requisições de sql.
		- O GraphQl permite que os clientes aninhem consultas e busquem dados de recursos em uma única solicitação.
		- <p><strong style="font-weight: 600">Vantagens:</strong></p>
			- É possivel adicionar novos campos e tipos a uma API GraphQL sem afetar as consultas existentes. Da mesma forma, depreciar os campos existentes é mais fácil.
			- Ao fazer análise de campo, um provedor de API pode descobrir quais clientes estão usando um campo. É possível esconder campos preteridos de ferramentas e removê-los quando nenhum cliente os estiver usando.
		- <p><strong style="font-weight: 600">Desvantagens:</strong></p>
			- Projetos do servidor GraphQL pode ser complexo para esquemas de dados muito complexos.
			- Custo de processo de operações complexas de atualizações (Mutations) pode ser um problema na escalabilidade do servidor.
	- <p><strong style="color: #689d6a">WebSocket</strong></p>
	  collapsed:: true
		- Protocolo desenvolvido para facilicar comunições entre o servidor e o cliente.
		- <p>O <span style="color: #d65d0e">Websocket</span> possui uma <strong style="color: #b16286">abordagem orientada a eventos</strong>, o que permite uma comunicação bidirecional sobre um canal permanente estabelecido entre o cliente e servidor.</p>
		- O Websocket é um protocolo usado para estabelecer um canal de comunicação de streaming bidirecional sobre uma única conexão de Protocolo de Controle de Transporte (TCP).
		- Também é utilizado as vezes para comunicação servidor-servidor.
		- <p><strong style="font-weight: 600">Vantagens:</strong></p>
			- WebSockets podem habilitar a comunicação full-duplex (servidor e cliente podem se comunicar simultaneamente) com baixo custo.
			- São projetados para trabalhar sobre a porta 80 ou 443, para operar o WS (WebSocket) o WSS (WebSocket com pilha de segurança), o que evita problema de firewalls.
			- São ótimos quando se quer fazer comunicação de streaming, transmissões ao vivo e conexões de longa duração. Embora, não seja um cenário apropriado quando se tem muita intermitência no cliente, o que pode ocasionar na desconexção do cliente.
- ## **Unidade 4 - Microsserviços**
  collapsed:: true
	- <p>Microsserviços é uma forma particular de projetar aplicações de software como suítes de serviços implantáveis de forma independente.</p>
	- Surgiu como um movimento de neǵocio, devido ao desafio de como implantar software mais rapidamente.
	- O conceito de microsserviços se popularizou com a publicação do aritgo de Martin Flowlr em 105 - https://martinfowler.com/articles/microservices.html
	- Monolito não é um código ruim, é apenas um código que é implantado com um único bloco num ambiente de produção, isso muitas vezes dificulta para que esse processo seja rápido.
	- <strong style="color: #d79921">Características</strong>
	  collapsed:: true
		- serviços como componentes (ao invés de bibliotecas) são publicados de maneira independente.
		- os serviços precisam denotar capacidade de negocio (ex: gestao de pedidos)
		- <p>interface publicadas (APIs) --> representa um sub conjunto das interfaces dentro de uma aplicação, ela é versionada e ela tem um endpoint que registro local daquele interface (conceito mandatório).</p> > Uma interface publicada da mais controle para que se possa mexer em várias partes da aplicação sem impactar outras partes. A utilização de APIs como REST, RPC ou GraphQL vai habilitar um conceito de uma interface publicada.
		- base de dados proprias --> flexibilidade, proteção modular, menor acoplamento.
		- <p>implantação automatizada</p> > <p><strong>Obs:</strong> Microsserviços implicam em uma agenda DevOps (pipeline automatizada, compenentes hospedados em conteineres - Docker).</p>
		- inteligência nos endpoints (APIs) --> unico ponto de contato para alguém ler ou enviar informações ou comandos para um microsserviço.
		- controle descentralizado de linguagens (linguagen poliglotas) e de base de dados (persitencia poliglota)
	- <strong style="color: #d79921">Razões para uso:</strong>
	  collapsed:: true
		- custo elevado de aplicações com arquitetura monolitica para alterar e implentar em produção
		- servidores web e de aplicação compartilhados com outras aplicações
		- longos ciclos de mudança
		- dificuldades de implantação
		- custo de evolução do legado
	- proteção modular --> arquitetura com baixo acoplamento e alta coesão
	  collapsed:: true
		- Em um mecanismo assincrono, uma interface publicada (API) é um contrato de uma mensagem que esta dentro de um fila de mensagens.
	- modelo conceitural --> https://github.com/dotnet/eShop
	- Com o modelo de microsservço, cada serviço será empacontado para poder ser implantadno de uma forma independente.
	- cada micro serviço opera de um forma independente, tipicamente ele é hospeado em um container como elemento de virtualização.
	- <strong style="color: #d79921">API Gateway</strong>
	  collapsed:: true
		- API Gateway em arquitetura possui dois significados: padrão arquitetural que irá isolar o front do back; produto de mercado que irá implementar esse padrão arquitetural. Exempplso de productos de mercado: API G, Amazon API Gateway, etc..
		- Papel do gateway: segrança --> separanda um rede desmilitarizada de internet da rede militariza, onde terá IP privativos dentro de um endereçacamento de rede proprietário, controle de acessos, observabilidade e auditoria dos acessos, mecanismo ligados a monetização.
		- O API Gateway pode fornecer a cada tipo de aplicativo cliente, interfaces proprias chamadas de BFF (Backend for frontend) --> padrão arquitetural muito usado em microsserviços quando se expoe um conjunto particular de endpoitns para uma aplicação.
		- microsserviços podem chamar outros microsserviços atraǘes de RPC, chamdas ligadas a rest. Em arquiteturas de larga escla é mais comum que se utilize arquitetura orientada por eventos --> tem se a figura de um servidor de fila de mensagens ou de streaming que ira fazer a comunicação assincroan entre mensagens dos váriso microsserviços.
	- estrangular monolito --> mover de um monolito para uma arquitetura de microsserviços.
	- A adoção de uma arquitetura de microsserviços precisa fornecer autonoma técnica para os times.
	- Governança técnica descentralizada é abordagem recomendada para equipes operando com microsserviços.
	- Plataforma CNCF (Cloud Native Computing Foundation) --> fornece uma coridoria de mais de 1000 tecnologicas organziadas em domínios.
	- <strong style="color: #d79921">Gestão de Dados Descentralizada</strong>
	  collapsed:: true
		- Em microsservicos a gestão de dados se torna descentrliada
		- Microsservicos preferem permitir que cada serviço gerencia sua propria base de dados, váriso bancos de dados lógicos particulares privativos a um determinado microsserviços. --> exigencia para arquitetura de microsserviços. Cada base de dados pode utilizar a mesam tecnologia de bd atraves de diferentes instancias, ou usando diferentes sistema bd --> abordagem Polyglot Persistence.
		- --> Uma base de dados proprietária para cada microsserviço não implica que cada micosserviço use um servico de bando de dados dedicado.
		- two face commit --> tranasacoes distribuidas, usando protocolo XA
		- Muitas tecnolgias de bando de dados NoSQL não dao suporte a transaçoes distribuidas.
		- O controle transacional é resolvido atraves de uma coordenaçao logica normalmente levado para o código.
		- Padrao arquiterual SAGA -- representa o conceito de uma coordenaçao de operaçoes que irao ocorre sobre multipleos microsserviços.
			- terá um conjunto de transacaoes que correm de forma local e algum tipo de coordenação que vai alem da transacao local.
			- padrao arquiterual de microsserviço
			- há duas forma de implementar:
				- Coreografia --> as partes operam de forma distriuida;
				  logseq.order-list-type:: number
				- orquestração --> implica em uma centralização; a saga é o loca de centralizaçõa da informação - o controle lógico da transacao esta dentro da saga, o papel da saga é simular o que teria em um banco de dados tradicional como controle transacional. não há uma consistencia de tempo real e sim uma concistencia eventual (latencia de milisecundos entre a informação) --> efeito colteral necessário quand ose desenvolve microsserviços.
				  logseq.order-list-type:: number
			- --> Em um abiente distribuido pode haver microsserviços operando em ladaso positos do planeta.
		- com,plexidades acidentais devem ser resolvidas com padoers como SAG e o CQRS.
		- O padrão arquitetural CQRS pode ser usado para proteger a escala da aplicação.
		- Segregação de Responsabilidade enttre Consultas, Queries e Comandos. O CQRS irá segregar os comandos de atualização dos dbs, dos comandos de consulta. Vou criar uma base denormalizada de historicos de pedidos -- essa base será alimentada atraves de eventeos que vao chegar dos varios microsservicos de tempos em tempos --> depedende da logica de negócio.
		- como há uma base denormalizada orientada a consulta, posso criar metodos de pesquisas que serão efeiticientes em buscar informação qu esta na base desnormalizada. banco de dados que opeream como cash distribuidos (redis, mongo,tecnologis de núvem).
		- Com CQRS vc protege a sua aplicação de microsservicos dados que wueries epsados vao acontencer contra uma banco de dados desnormaliada --> muito utilizado em arquteturas distribúidas.
		- Banco de dados por servico:
			- vangatens:
				- descopament opode ser relizado - alteração de bancos de dados não afetam outro bd
				- cada serviço pode usar o tipo de bando de dados mais adequado a suas necessidades
				- um serviço que faz pesquisas de testo poder usar o ElasticSearch
				- Um serviço que maniupla um grafo social poderia usar Neo4j
			- desvantagens:
				- a implementaçãies distribuids que abrangem vários sercios não é simples.
				- a implementação de consultas que associam dados que estão em vários banco de dados é um desafio.
				- complexidade do gerenciamento de vários banco de dados SQL e NoSQL
	- <strong style="color: #d79921">Padrões Arquiteturais</strong>
	  collapsed:: true
		- Padrão arquitetural é uma melhor prática, é algo que foi descoberto no mercado e que se tornou uma melhor prática para se lidar com um certo problema que emege em um determinado domínio.
		- Todo padrão possui uma lingaguem comum para descreve-lo (Contexto, Problema, Solução).
		- Plataforma web --> microservices.io/patterns
		- Quando uma grande coleção de padrões são combinados tem-se uma linguagem de padrões.