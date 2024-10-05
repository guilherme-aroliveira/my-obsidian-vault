## **Unidade 1**
collapsed:: true
	- <p>Cada browser possui seu <span style="color: #d65d0e">motor de interpretação</span> (browser engine) de códigos de <span style="color: #d65d0e">Front-End</span>, isso implica em algumas diferenças relacionadas ao desempenho (performance) ou diferenças visuais para o usuário final.</p>
	  collapsed:: true
		- <p>Chrome e Edge: <span style="color:#689d6a">Chromium</span></p>
		- <p>Firefox: <span style="color:#689d6a">Gecko</span></p>
		- <p>Safari : <span style="color:#689d6a">WebKit</span></p>
	- <p><span style="color:#689d6a">V8 Engine</span> <span style="color: #3588E9">--></span> motor criado pela Google que deu origem a plataforma Node, uma possibilidade de interpretar JavaScript no lado do servidor.</p>
	- Dinâmica de <strong>processamento do Browser</strong>:
	  collapsed:: true
		- <p><strong style="color: #d79921">Load HTML</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Parse HTML</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Load CSS</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Parse CSS</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Create DOM tree</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Display</strong></p>
		- <p><span style="color: #3588E9">--></span> Com o protocolo <span style="color: #d65d0e">HTTP 2.0</span> é possivel fazer o carregamento do CSS em paralelo.</p>
	- <p><span style="color: #3588E9">--></span> A <span style="color: #d65d0e">arvore de elementos DOM</span> é basicamente a estrutura de elementos html, mas que já foi processado no browser.</p>
	- Blocos de estilos possuem um desempenho melhor, pois não será feita uma novo requisão para o código CSS.
	- <p>Os <span style="color: #d65d0e">frameworks</span> de Front-Ends mais utilizados no mercardo brasileiro são: <span style="color:#689d6a">Angular</span>, <span style="color:#689d6a">Vuejs</span>, <span style="color:#689d6a">ReactJs</span>.</p>
	- <p>Plataforma para testar vários frameworks <span style="color: #3588E9">--></span> <a href="https://codesandbox.io/"><span style="color:#98971a">code sandbox</span></a></p>
	- <p><strong style="color:#689d6a">Angular</strong>:</p>
	  collapsed:: true
		- É um framework open-source criado pela Google para simplificar a construção de aplicações Web.
		- <p>Foi criado para o desenvolvimento de aplicações de ponta-a-ponta. Muitas das bibliotecas e recursos já são nativos do angular, como por exemplo: sistemas de rotas, arquitetura e organização de pastas sugeridas, sugestão de uso dos <span style="color:#98971a">Services</span> para consultas a APIs externas.</p>
		- <p>Utiliza uma linguagem tipada (<span style="color:#689d6a">typescript</span> <span style="color: #3588E9">--></span> possui recursos a mais do que o javascript).</p>
		- Foi desenvolvido para permitir que o desenvolvedor foque na lógica do negócio.
		- <p>Estão presentes do Angular, conceitos e recursos de linguagens de backend (Java, C#), como interface, tipos genereticos, decorators, orientação a objetos.</p>
		- É necessário que se saiba os conceitos core do framework: componentes, diretivas, módulos, serviços, proramação reativa com RxJs, injeção de dependencia, httpclient.
		- <p>Possui um utilitário de linha de comando que permite criar partes da aplicação <span style="color: #3588E9">--></span> <span style="color:#98971a">angular-ci</span></p>
		  collapsed:: true
			- Essa ferramenta permite criar componentes, serviços, módulos e diretivas.
			- Exemplo: `ng generate component my-component`
		- <p>Possui bilbiotecas de componenetes <span style="color: #3588E9">--></span> <a href="https://material.angular.io/"><span style="color:#98971a">angular-material</span></a>.</p>
		- É uma linguagem mais verbosa, necessário mais linhas de código para escrita da aplicação.
		- É bastante utilizado para aplicações web corporativas (ERP, Dashboards) e para aplicações de grande porte em geral.
	- <p><strong style="color:#689d6a">Vue</strong>:</p>
	  collapsed:: true
		- É um framework focado para a criação de componenetes web, por isso que os recursos iniciais possuem o básico para a criação de componentes.
		- A <strong>instalação padrão</strong> (default) tem como único recurso possível, a criação de componentes.
		- Foi desenvolvido para que seja adotado de forma incremental.
		- <p>Embora não tenha sido para o desenvolvimento de <span style="color: #d65d0e">SPAs</span> (Single Page Applications), é possivel desenvolve-las instalando bibliotecas externas:</p>
		  collapsed:: true
			- <p><span style="color:#98971a">Vue-router</span> <span style="color: #3588E9">--></span> possibilita o gerencimaento de rotas.</p>
			- <p><span style="color:#98971a">Vuex</span> <span style="color: #3588E9">--></span> possibilita p gerenciamento de estados.</p>
		- <p><strong>Todo</strong> o código relacionado a um componente pode ser escrito no mesmo arquivo.</p>
		- <p>Possui um formato de arquivo próprio <span style="color: #3588E9">--></span> <span style="color: #d65d0e">.vue</span></p>
		- Permite a escrita de CSS com escopo de forma nativa, e também permite a configuração da aplicação para aceitar a escrita dos componenetes em Typescript.
		- <p>Possui bibliotecas de componentes para agilizar o desenvolvimento das aplicações <span style="color: #3588E9">--></span> Ex: <a href="https://www.creative-tim.com/vuematerial"><span style="color:#98971a">vuematerial</span></a></p>
		- O padrão de desenvolvimento fica a cargo do desenvolvedor.
		- Os componentes devem ser separados em partes mais pequenas, pois os arquivos dos componentes tende a crescer exponencialmente.
		- Usos mais comuns: desenvolvimento de bibliotecas de componentes cross-framework; componentização de aplicações já existentes; criação de aplicações de pequeno porte.
	- <p><strong style="color:#689d6a">React</strong>:</p>
	  collapsed:: true
		- É um framework mantido pelo Facebook, totalmente focado em componentes (no React, tudo é um componente).
		- Foi concebido inicialmente para o desenvolvimentos de interfaces de usuário.
		- Para criar coisas mais avançadas é necessário instalar bibliotecas externas.
		- <p>Utiliza a lingaguem <span style="color:#689d6a">JSX</span>, embora seja possivel criar um código HTML dentro de um arquivo de componente.</p>
		- <p><span style="color: #d65d0e">JSX</span> <span style="color: #3588E9">--></span> É uma extensão JavaScript que permite a criação de árvores Document Object Model (DOM) usando uma sintaxe semelhante a XML. </p>
		- <p>Foi o primeiro framework a implementar o conceito de <span style="color: #d65d0e">Virtual DOM</span> <span style="color: #3588E9">--></span> o componenete renderizado pelo o usuário é comparado como o que que será atualizado. Permite mais desempenho.</p>
		- <p>Permite a integração o <span style="color:#689d6a">TypeScript</span> <span style="color: #3588E9">--></span> há no github uma base do React já configurado com o typescript.</p>
		- Permite a criação de aplicações SPA através de bibliotecas da comunidade (Ex: react-router).
		- Utilizada um paradigma de escrita de componenetes diferentes de outros frameworks.
		  collapsed:: true
			- Exemplo: `const MyComponent = () => <h1>Hello World</h1>`
			- Exemplo mais tradicional:
			  collapsed:: true
				- ```jsx
				  function App(props) {
				  	return (
				      	<div className="App">
				            <h1>{props.title}</h1>
				            <h2>Start editing to see some magic happen!</h2>
				         	</div>
				      );
				  }
				  ```
		- <p><span style="color: #3588E9">--></span> Todos os componenetes em React são funções.</p>
		- <p>Embora não possua mecanismo nativo para gerência de estados da aplicações, através da biblioteca <span style="color:#689d6a">Redux</span> (criado por um dos engenherios envolvidos na criação do React) é possivel realizar o gerenciamento de estados.</p>
		- <p>Possui uma boa integração com a linguagem <span style="color:#689d6a">FlowTyped</span> (linguagem tipada).</p>
		- <p>Um mesmo componente pode ser escrito de diversas formas, tais como: funções, classes e funções com hooks.</p>
		- Utiliza vários conceitos de programação funcional. Pode ter os componenetes escritos em funções.
		- Possui a maior comunidade e tudo já foi feito por alguém no StackOverflow.
		- Esta em constante evolução, e as evoluções foram tratadas de formar a manter uma maior retrocompatibilidade.
		- Usos mais comuns: criação de bibliotecas e componentes, aplicações de grande porte, aplicações que possuem uma versão mobile, desenvolvimentos de aplicações focados em desempenho.
	- <p><span style="color: #d65d0e">Single Page Application</span> <span style="color: #3588E9">--></span> são aplicações que interagem com o usuário reescrevendo o conteúdo da página atual, sem a necessidade de recarregar a página inteira. Possuem uma sensação de fluidez, pois apenas o conteúdo principal é trocado nas mudanças de páginas.</p>
	- <p><strong style="color:#689d6a">Criando uma SPA</strong>:</p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">API</span> gratuita <span style="color: #3588E9">--></span> <a href="https://www.themoviedb.org/"><span style="color:#98971a">the movie database</span><a></p>
		- <p><span style="color:#689d6a">create-react-app</span> <span style="color: #3588E9">--></span> ferramenta para criar aplicações em React.</p>
		- <p>npx <span style="color: #3588E9">--></span> comando para criar</p>
		- instalação de 3 bibliotecas:
		  collapsed:: true
			- <p>react-router-dom --> para</p>
			- <p>styled-components --> para estilizar a aplicação via css e js</p>
			- <p>axios --> para realizar aquisições na API externa a ser consumida</p>
			- <p>para instalar as biliotecas --> npm i react-router-dom styled-components axios</p>
		- <p>Para rodar o servidor da aplicação <span style="color: #3588E9">--></span> <span style="color:#689d6a">npm start</span></p>
		- <p>map() --> função do javascript que itera e modifica os elementos</p>
		- Em uma arquitetura SPA as rotas são definidas no Front-End, sendo que cada rota terá um comportamento diferente.
		- Os elementos no React precisam de ter um único elemento raiz
- ## **Unidade 2**
  collapsed:: true
	- <p><strong style="color:#689d6a">CSS</strong></p>
	  collapsed:: true
		- Esta ligado diretamente ao desempenho e a escala.
		- Override de estilos é custo para o browser.
		- Manter a consitência de estilos entre as telas é de suma importância.
		- Definir uma metodologia adequada de nomeclatura de classes.
		- <p><strong style="color: #d79921">Style-guides</strong> (padrão de escrita CSS) e metodologias:</p>
			- <p><strong style="color: #3588E9">BEM: Block - Element - Modifier</strong></p>
			  collapsed:: true
				- Block: header, container, menu, checkbox, input
				- Element: itens de um bloco (item de menu, item de lista, título de cabeçalho)
				- <p>Modifier: estado em que o elemento ou bloco se encontra<ul><li>Exemplos: disabled, active, fixed, background cinza</li></ul></p>
				- <p>Exemplos de tecnica kebab-case:<ul><li>main-nav</li><li>main-nav__item --> indica um elemento que percente ao main-nav</li><li>main-nav__item--is-active</li></ul></p>
				- documentação --> http://getbem.com/naming/
			- <strong style="color: #3588E9">OOCSS: Object-Oriented CSS</strong>
			  collapsed:: true
				- Separação entre o CSS de estrutura e skin
				- <p>Structure properties:<ul><li>Width | Height | Padding | Margins | Overflow</li></ul></p>
				- <p>Skin (propriedades visíveis para o usuário):<ul><li>Color | Background | Front | Shadow</li></ul></p>
				  collapsed:: true
					- <p>Exemplo:</p>
						- ```css
						  .skin-1 {
						    background: white;
						  }
						  
						  .skin-2 {
						    background: black;
						  }
						  
						  .button {
						    width: 50px; height: 50px;
						    border-radius: 5px;
						  }
						  ```
						- ```html
						  <button class="button skin-1">Botão<button>
						  ```
				- Separação do container do conteúdo
				- Ausência de classes herdadas --> para que se possa reutilizar qualquer conjunto de estilos para qualquer elemento futuramente.
				  collapsed:: true
					- Exemplo:
						- ```css
						  .sidebar-container {
						    position: absolute;
						    padding: 2px;
						    margin: 3px;
						    left: 0;
						  }
						  
						  .sidebar {
						    width: 140px;
						  }
						  
						  .list {
						    margin: 3px;
						  }
						  
						  .list-header {
						    font-size: 16px;
						    color: red;
						  }
						  ```
			- <strong style="color: #3588E9">CSS Functional:</strong>
			  collapsed:: true
				- Ideia de ter micro classe de CSS para compor um único elemento;
				- Cada classe altera uma única propriedade do CSS;
				- Classses sempre tratam reponsividade desde a concepção;
				- <p>Frameworks: Tachyons | Tailwind CSS | BassCSS</p>
				  collapsed:: true
					- Tachyons
						- ```css
						  :root {
						    --spacing-none: 0;
						    --spacing-extra-small: .25rem;
						    --spacing-small: .5rem;
						    --spacing-medium: 1rem;
						  }
						  
						  .pa0 { padding: var(--spacing-none); }
						  .pa1 { padding: var(--spacing-extra-small); }
						  .pa2 { padding: var(--spacing-small); }
						  .pa3 { padding: var(--spacing-medium); }
						  ```
						- ```html
						  <div class="w-10 tl pa1">
						      Conteúdo do elemento aqui
						  </div>
						  ```
				- Características do CSS funcional:
				  collapsed:: true
					- Responsividade: todas as lcasses possuem tratamento reponsivo;
					- Reutilizável e modular: inumeras classes prontas para serem usadas em qualquer tela;
					- Legibilidade: ao olhar o HTML, voce sabe examente qual sera o seu estilo;
					- Produtividade: escrever HTML é mais rápido, pois diminui a necessidade de criar classes para modificar propriedades simples
			- <strong style="color: #3588E9">CSS-in-JS</strong>
			  collapsed:: true
				- Formato de escrita de CSS em arquivos JavaScript;
				- Classes CSS podem ser escritos em formato de função, que são traduzidos em componenetes posteriormente;
				- CSS dinâmico: uma classe CSS pode se comportar de forma diferente de acordo com os parâmetros que são passados.
				- O proprio framework gera uma classe aleatória (hash aleatorio), que impede colisão de nome de classes. Esse mecanismo é tratado de forma automática.
				- --> O framework "style-components" consegue identificar alguams propriedade que não funccionam em um determinado browser, e adiciona alguns sufixos, para que a propriedade seja reconhecida pelor browser.
				- Exemplo no contexto do React:
					- ```css
					  import styled from 'styled-components'
					  
					  export const Header = styled.header`
					    background: black;
					    color: red;
					    font-size: 14px;
					  `;
					  ```
					- ```html
					  // JSX
					  <div>
					    <Header> 
					      Conteúdo do cabeçcalho aqui
					    <Header>
					  </div>
					  ```
		- <strong style="color: #d79921">Pré-processadores de CSS</strong>
		  collapsed:: true
			- permiti adicionar novos recurso na escrita de estilos
			- Tres principais ferramenta: SASS, LESS e Styles --> são extensoes utilizadas em tempo de desenvolvimento.
			- permite gerar CSS baseado em linguagem do pré-processador
			- Principais recursos: variáveis, mixins, escrita de estilos por herança
			- <p><strong style="font-weight: 600">Exemplo SASS - variáveis:</strong></p>
			  collapsed:: true
				- ```scss
				  // variables.scss
				  $primary-bg: 'green';
				  $primary-color: 'white';
				  ```
				- ```scss
				  @import "variables.scss";
				  
				  .main-nav {
				    background: $primary-bg;
				  
				    .nav-item {
				      color: $primary-color;
				    }
				  }
				  ```
			- <p><strong style="font-weight: 600">Exemplo SASS - Mixins:</strong></p>
			  collapsed:: true
				- É um recurso similiar a um procedimento no JavaScript - possibilidade de reutilizar código.
				- Permite ter uma bao escalabilidade na criação de recursos compartilhados
				- Complexidade: necessita de alguma ferramenta de build para interpretar os pré-processadores
				- ```scss
				  @mixin tranform($property) {
				    -webkit-transform: $property;
				    -ms-tranform: $property;
				    transform: $property;
				    }
				  
				  .box { @include transform(rotate(30deg)); } // @include --> chama a função
				  ```
			- <p>_file.css <span style="color: #3588E9">--></span> arquivo com underscore é um padrão para definir que o arquivo é um modulo que será importado em outro arquivo.</p>
	- <strong style="color:#689d6a">Bundlers</strong>
	  collapsed:: true
		- A ferramenta de build permite escrever HTML, JavaScript e SASS através de forma automatizada através de um arquivo de configuração.
		- Frameworks mais recentes possuem algum bundler embutido.
		- <strong style="color: #d79921">Webpack</strong>
		  collapsed:: true
			- bundler mais utilizado pela comunidade, é utilizado por Angular, Vue e React.
			- gera os arquivos concatenados e minificados.
			- <p>utiliza o conceito "convention over configuration" <span style="color: #3588E9">--></span> define um conjunto de regras</p>
			- no terminal: o comando webpack faz o build de um arquivo no diretório dist com bundle.js
			- <p><span style="color: #d65d0e">loaders</span> <span style="color: #3588E9">--></span> adicionam mais funcionalidades ao build</p>
				- <p>sass-loader <span style="color: #3588E9">--></span> loader responsável por compilar arquivos sass em css</p>
			- <p>arquivo de configuração <span style="color: #3588E9">--></span> webpack.config.js</p>
	- <strong style="color:#689d6a">Arquitetura Modular</strong>
	  collapsed:: true
		- <p><span style="color: #d65d0e">last reponsible moment</span> <span style="color: #3588E9">--></span> conceito de arquitetura evolutiva</p>
		  collapsed:: true
			- o projeto dever ser construido de forma que consiga sofrer alterações ao longo do seu ciclo de vida (escalável).
			- adidar as decisões arquiteturais sempre que possível (arquiterura flexível)
		- A arquitetura modular pode ser aplica a qualquer stack de tecnologia do front-end (agnóstica)
		- <p><strong style="color: #d79921">Proposta de arquitetura modular</strong> <ul style="list-style-type:disc"><li><span style="color: #98971a">UI Componenets:</span> contem a lógica visual e de interação com o usuário. Exemplo: Botoes, Menus, Cabeçalhos.</li><li><span style="color: #98971a">Page Components:</span> componenetes que representam uma tela e estão associados a uma rota. todas as telas estão associadas a um componente. Exemplo: tela de detalhes de um filme.</li><li><span style="color: #98971a">Application routes:</span> arquivo que contém todas as rotas daquele módulo. Toda nova rota (URL) deve estar associado a um componente.</li><li><span style="color: #98971a">API Client:</span> ponto único de contato entre a aplicação e API externa. Camada entre o componente e uma API externa (desacoplamento).</li><li><span style="color: #98971a">State management:</span> camada que permite compartilhar estados comuns entre os componentes. É mais comum em aplicações de maior porte.</li></ul></p>
			- Cada item será um diretório, e cada conjunto de pastas pode consituir um modulo. Exemplo: módulo de usuário que constitui das divisões de pastas, de forma que esse conjunto seja um módulo da aplicação.
			- <p><strong style="font-weight: 600">Exemplo:</strong> <ul style="list-style-type:disc"><li>/ => HomeComponent <span style="color: #3588E9">--></span> é o page componenete, o que estiver dentro dele são os UI Componenets</li><li>/about => AboutComponent</li><li>/products => ProductsComponent</li></ul></p>
			- <p><span style="color: #d65d0e">SSOT:</span> Single Source of Truth <span style="color: #3588E9">--></span> unica store que é reponsável por armazenar os dados que são compartilhados</p>
			- <p><span style="color: #d65d0e">arquitetura flux</span> <span style="color: #3588E9">--></span> para gerenciamento de estados</p>
			  collapsed:: true
				- utlizada em frameworks como o Redux, por exemplo.
				- o Redux é uma implementação da arquitetura flux
			- Opções de divisão de pastas: divisão por módulos ou divisão por dimínios.
			- smart compenents --> componentes que armazenam toda a logica de interação.
			- container components --> componenetes que montam os componentes que possuem logica de interação direta com o usuário.
			- --> cada modulo deve ser autonomo, e contem o seu proprio conjunto de responsabilidades.
	- <strong style="color:#689d6a">Arquitetura Flux</strong>
		- parte da ideia de arquitetura modular --> gerenciamento de estado
		- store --> armazena o estado de toda a aplicação
		  collapsed:: true
			- estado é atualizado a partir de algum dispatcher
			- comparada a um "estado global" --> multiplos lugares que podem atualizar o mesmo dado e que permite consumir dados de múltiplos lugares.
			- fluxo único para a UI
		- actions --> conteúdos enviados da aplicaçao para a store
		  collapsed:: true
			- descreve o que acontece
			- precisa ter um apropriedade "type"
			- <p>função que retorna um objeto de javascript</p> > ```javascript
			  const setUser = user => ({
			  type: SET_USER,
			  payload: user,
			  })
			  ```
			- a solicitação de uma alteração é sempre o usuário final.
		- reducers --> descreve como as alterações e os dados na store são transformados
		  collapsed:: true
			- recebe uma action como argumento
			- são funções puras (nada é alterado fora do seu escopo)
			- ```javascript
			  import { SET_USER } from '../actions';
			  
			  // logica gerenciada pelo Redux
			  function user(state = {}, action) { 
			    switch (action.type) {
			      case SET_USER:
			        return {
			          ... state,
			          user: action.payload
			        }
			      default:
			        return state
			    }
			  }
			  ```
- ## **Unidade 3**
  collapsed:: true
	- <strong style="color:#689d6a">Arquitetura de Micro front-end</strong>
	  collapsed:: true
		- ideia parecida com a de microsserviços no back-end
		- possibilidade de multiplos frameworks em uma mesma aplicação (arquitetura agnóstica)
		- pipelines mais rápidas e independentes (build, test e deploy)
		- <p><span style="color: #3588E9">--></span> quando maior a abstração, maior a complexidade do projeto</p>
		- <strong style="font-weight: 600">Definições</strong>
		  collapsed:: true
			- baixo acoplamento e alta coesão
			- isolar os projetos em bases de códigos diferentes
			- cada micro front deve ter uma base de código de independente
		- <strong style="color: #d79921">Implementações</strong>
			- <strong style="color: #aaaaff">Implementação em tempo de build</strong>
			  collapsed:: true
				- através de pacotes npm
				- cada dependencia é um micro-front diferente --> cada micro-font é pacote que esta publicado no npm
				- npm --> gerenciador de móduloes do Node
				- é possivel publicar um projeto de forma privada no npm (utiliza um token de acesso)
				- a pipeline de build, test e deploy é independente, mas em partes (é necessário atualizar toda a aplicação)
			- <strong style="color: #aaaaff">Integração por meio de funções javascript</strong>
			  collapsed:: true
				- cada script é um projeto autonomo
				- cada script deve disponibilizar um função de renderização de um determinado micro front
				- para cada rota há uma função --> cada função é responsável por renderizar um micro front
				- uma "div" é utilizada na chamada de uma função para renderizar um micro front
				- <p>artigo --> <a href="https://martinfowler.com/articles/micro-frontends.html">martinfowler</a></p>
			- <strong style="color: #aaaaff">Integração através de web components</strong>
				- embarcar uma parte do projeto dentro de um web-component
				- --> o web-component é cross-framework e independente de frameworks
				- funções em escopo global podem ser definidas para comunicar entre os micro front
			- <strong style="color: #aaaaff">Integração via iframes</strong>
			  collapsed:: true
				- <p>cada iframe carrega uma URL</p> > ```html
				  // about page
				  <div id="container">
				    <iframe src="https://about.project.com"></iframe>
				  </div>
				  ```
	- <strong style="color:#689d6a">Arquitetura de monorepos</strong>
	  collapsed:: true
		- estilo arquitetural para construção de aplicações front-end
		- conceito arquitetural que propoe uma repositório para múltiplos pacotes
		- cada pacote representa um projeto (micro frontend ou módulo)
		- ferramentas: lerna e yarn workspaces
	- <strong style="color:#689d6a">Aplicações Server-Side Rendering</strong>
		- o servidor é responsável por exibir o conteúdo para o cliente
- ## **Unidade 4**
  collapsed:: true
	- Aplicações PWA
		- PWA --> Progressive Web Application
	- Web Assembly
	- Segurança em front-end
		- OWASP
		- OWASP TOP TEN