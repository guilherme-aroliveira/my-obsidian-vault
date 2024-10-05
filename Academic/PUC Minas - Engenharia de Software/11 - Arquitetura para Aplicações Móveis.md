## **Unidade 1 - Fundamentos**
	- <p>Computação móvel (CM) --> area da tecnologia que amplia o domínio da Computação Distríbuida.</p> > A computação móvel é um caso especial de computação distribuída onde os problemas de conexão e desconexão são contantes.
	- Desafios da CM: interface, processamentos, comunicação, energia, segurança.
	- Conceito de redes celulares surgiu em 1947 nos laboratórios Bell (EUA).
	- Rede Celular - Componentes:
		- Dispositivo móvel
		- Antena --> faz a tranmissão com o celular
		- MSC (Mobile Swiwthing Center) --> respinsável por levar a conexão da Antena até a Central de Comutação de Telefonia Pública.
		- PSTN (Public switched telephone network) --> consegue a rede movel com outras redes.
		- --> Para gerar eficiencia operacional, muitas empresas compartilham a mesma estrutura de Antena.
		- redes --> PSTN --> MSC --> [Antena -- dispositivo móvel]
	- Rede Celular - Caracteristicas:
		- Roaming --> permite que um usuário utilize o telefone celular fora da área de cobertura de sua operadora. Exemplo: uso do telefeone em outros país. Obs: No Brasil os usuários não são tarifados pelo uso de roaming, por causa dos acordos comerciais entre as operadores.
			- pode utilizar a infraestrutura de outra operadora
			- envolve custos adicionais para o usuário
		- Controle de Energia --> a rádio-base e a estação celular podem determinar o uso de energia (potência do sinal) do telefone celular.
		- Reuso de Frequencia --> células adjacentes utilizam canais diferentes.
		- Handoff --> É a passagem, de forma transparante, de um usuário móvel de um célula para outra, ou seja, é a capacidade de trafego entre rádio bases sem que haja a interrupação do serviço.
			- Controlado pela Rede: realizado de forma centrliazda. A MSX toma a decisão de fazer o handoff.
			- Handoff assistido: O telefone celular auxilia a MSC fazendo mediações do sinal para sinalizar o handoff.
			- Controlado pelo telefone celular: a estação móvel toma a decisão de solicitar o handoff para a estação rádio-base.
			- Tipos de Handoff:
				- Soft --> a transiÇão ente uma celula e outra é relizada de forma suave. Exemplo: corta um pouco a voz ou acelera a voz.
				- Hard --> ocorre uma pequena interrupção durante a mudança de células (perda de dados). Pode ocorrer perda de conexão.
	- 5G --> traz velocidades acima de 10 gigabit por segundo, permite a conexão de 1 milhão de dispositivos a cada quilometro quadrado e menor latência.
	- Segurança e Privacidade
	  collapsed:: true
		- O smartphone traz caracteristicas de vazamento muito mais latentes do que se tem na web e em sistemas desktop, porque dentro do aplicativo móvel há muitos dados sensiveis.
		- Proteção insuficiente da camada de trasnporte
			- A camada de transporte deve ter pelo menos um SSL ativo. Os conteúdos devem trafegar uma criptografia forte, padrão da ind;ustria e comprimenos de chave apropriados.
			- Nunca permitia certificados autoassinados
		- Armazenamento de dados de forma insegura pelo app
			- Exemplo: tokens de autentiação, senhas, cookies, dados de localização, dados pessoais.
			- não armazene dados confidenciais 9por exemplo, credenciasi no dispositivo.
			- criptografe todos os dados.
		- Outros ataques que ipactam o desenvolvimento do app:
			- auttorização e autenticao deficientes --> tokens
			- criptgorafia quebrada --> usar padrão da insduatria (criptgrafia por comparações), levar para núvem
			- decisao de segurança por meios de entradas não confiáveis
			- manuseio improprio da sessao
			- engenharia reversa
		- --> os apps moveis tem a presença de ataques classicos de outros tipos de app. Tais como: SQL Injection, Cross-Site Scripting, Malware, Phishing e Ransonware.
- ## **Unidade 2 - Sistemas Operacionais e Arquitetura**
	- Sistemas Operacionais
	  collapsed:: true
		- iOS --> sistema operacional para dispositivios móveis da Apple.
		  collapsed:: true
			- ótimo gerenciamento da memória
			- compatiblidade específica com o hardware
			- integração com outros dispositivos Apple
			- xCODE --> plataforma de desenvolvimento
			- Camadas do sistema operacional: [Application] -- [Media] -- [Core Services] -- [Core OS] -- [Kernel]
				- a camada da aplicação consume caracteristicas Media e Core Services
				- o Kernel e Core OS não é acessível pela aplicação
		- Android --> sistema operacional baseado em Linux
		  collapsed:: true
			- desenolvido pela Google
			- estremamente flexível
			- código aberto
			- liberdade de customização e configurações
			- Camadas do sistema operacional: [Applications] -- [Application Framework] -- [Libraries] -- [Android Runtime] -- [Linux Kernel]
				- as camadas Libraries e Android Runtime são de acesso do sistema
				- é possivel acessar a camada de Kernel através do Root (acesso de administrador)
		- Chrome OS --> sistema pela Google baseado em Linux
		  collapsed:: true
			- utiliza o Google Chrome como principal interface de usuário
			- suporta primariamente aplicativos da web
			- pode ter PWA instalado (html5)
			- bateria de grande duração
			- menos suscetível a vírus
		- Tizen OS --> sistema operaciona de código aberto Linux
		  collapsed:: true
			- desenvolvido pela Linxu Foundation em parceria com a Samsung, Panasonic e Intel
			- facilita o desenvolvikento de aplciações nativas e html5
			- boa documentação de APIs
		- webOS --> sistema operaciona da LG
		  collapsed:: true
			- permitir desenvolver em html5 ou em Java
			- possui um modo de privacidade aprimorada
	- Aplicativo Nativo
	  collapsed:: true
		- Aplicativo de smartphone codificado em uma linguagem de programação específica.
		- Desvantagens: colabodores especializados e escassos, precisa de suport para framework, maior prazo de desenvolvimento, maior custo de desenvolvimento.
		- São desenvolvidos quando é necessário uma aplicação de alta performance
		- As camadas de um app nativo irá depender do estilo arquitetural adotado (Exemplo: MVC)
		- --> A linguagem Kotlin mantêm interoperabilidade direta com o código Java (aplicações legadas), é multiplataforma e consegue entregar regra de negócio para o iOS.
		- Caso Netflix: uso do Kotlin para desenvolver a regra de negócio tanto para Android quanto para iOS.
	- Aplicativo Hibrído
	  collapsed:: true
		- Com um app híbrido o projeto funciona em múltiplos sistemas operacionais
		- --> A definição arquitetural deve ser antes de começar a desenvolver a aplicação.
		- hibrído de html5 --> conteúdo é em html5+css+js e conversa com o dispositivo através de plug-ins (ex: Ionic)
		- cross platform --> podem usar uma linguagem de terceiros, mas uma compilação prévia gera os cógigos nativos das plaforma (Ex: Flutter)
		- <p><strong style="font-weight: 600">Vantagens:</strong> <ul><li>permite comunicação com hardware via plugins ou traduação para código nativo</li><li>integração com a UI --> cross platform e frameworks</li><li>funciona de modo off-line</li><li>desenolvimento mais rápido com equipes integradas</li></ul></p>
		- <p><strong style="font-weight: 600">Desvantagens:</strong><ul><li>não entrega o máximo de performance que o dispositivo pode oferecer</li><li>os códigos são padronizados para as funções que existem em todas as plataformas</li><li>não permite alta integração com o S.O.</li></ul></p>
		- --> Para criar um aplicação mais pesada o hibrído de html5 terá 3 camadas - [HTML5]---[Plugins]---[API do dispositivo]
		- O app hibrído de html5 tem uma performance deficitaria.
		- O app cross platform em termos de desempenho é mais funcional.
		- Apps nativos são mais indicados para sistemas legados, alta demanda de desempenho, correções de path de segurança.
		- Apps hibrídos são mais indicados para startups.
	- Web App e PWA
		- Web App --> principal característica é a responsividade, controles voltados ao mobile. Utiliza 100% do que o navegador oferece.
		- PWA (Progressive Web App) --> evoluação do Web App, é mantido pela Google. É possivel relizar push notification, cache, disponibilidade off-line, serviços em background, instalação com característica de um app nativo/hibrido. Tem compatibilidade de 100% com o Android.
			- É uma pagina web desenhada com características de uma aplicação móvel. Através de um service worker que fica instalado dentro do navegador mobile, ele consegue fazer algumas interações que aplicativos consegue.
			- O service worker é um aplicativo que roda em background dentro do navegador que é reponsável por fazer o cash.
		- <p><strong style="font-weight: 600">Vantagens:</strong> <ul><li>Multiplataforma</li><li>Tecnologias já conhecidas</li><li>Fácil manutenção para todos os sistemas</li><li>Custo mais baixo</li><li>Tempo de produção baixo</li></ul></p>
		- <p><strong style="font-weight: 600">Desvantagens:</strong> <ul><li>Baixa integração com o S.O</li><li>Baixo desempenho</li><li>Alto consumo de dados</li><li>Nãp funciona sem conexão de dados (Web App)</li><li>Não acessa os periféricos dos dispositivos</li></ul></p>
- ## **Unidade 3 - Tópicos Especiais**
	- Padrões de Projeto
	  collapsed:: true
		- Separação de conceitos --> significa que diferentes entidades devem ser separadas no código.
		- Para que os testes sejam realizados de maneira eficaz, é importante ter um padrão de projeto/software. Com uma arquitetura adequada é muito mais fácil realizar as metodologias de teste.
		- O aplicativo deve ter uma base solida para o desenvolvimento de novos recursos e mudanças de acordo com as necessidades do negócio. Também deve ser adequado para futuras renovações --> Escalabilidade
		- Uma boa arquitetura simplica o código para escrita e leitura --> manutenção
		- --> Uma arquitetura bem construída possibilita uma longevidade maior e um processo de integração melhor com as tecnologias mais atuais.
		- <p>Desafios: servicos de terceiros (pagamento, login, etc), complexidade de navegaçãom formataçao de dado; nivel de habilidade de uam equipe, limites de tempo e orcamento.</p> > <p><strong>Note:</strong> link com a tecnologia --> dentro de SO/plataforma, qual é a tecnologia mais adequada para se construir uma aplicação.</p>
		- --> Cada padrão de projeto pode ser implementado em todas as linguagens, mas alguns padrões de projeto se acomodam melhor com um tipo melhor de linguagem. Exemplo: O padrão MVVM é muito uilizado no iOS, mas ele também pode ser usado com Android.
		- MVC
		  collapsed:: true
			- funciona muito bem para projetos pequenos
			- deve-se mapear claramente qual view esta utilizando o controlador.
			- bastante utilizado caso seja preciso fazer algo mais rápido
			- é uma padrão muito utilizado se não há muita interface, se não há um fluxo de informação muito complexo.
		- MVP
		  collapsed:: true
			- derivado do padrão MVC, muitas vezes tratado com uma evolução.
			- possui uma testabilidade melhor que a do MVC, mas ainda limitada.
			- não é aconselhável que seja utilizado em uma aplicação com mais de 15 telas de UI.
			- a view é responśavel apenas pelo desenho do componente e integração de dados.
			- reuso de código pode ser feito, mas esse reuso de código pode ser benefico ou não, dependendo do tamanho da aplicação.
		- MVVM
		  collapsed:: true
			- permite separar a lógica da UI da lógica de negócios.
			- tecnicas de implementação: Android - LiveData e Observers, iOS Swift com Data Bindings
			- --> cada linguagem terá seus mecanismos tecnicos para que seja feita a implementação de um padrão de projeto.
- ## **Unidade 4 - Construíndo uma experiência mobile com PWA**
	- O index.html é responsável por declarar o service worker
	- service worker não é registrado no DOM do javascript --> é registrado no navegador