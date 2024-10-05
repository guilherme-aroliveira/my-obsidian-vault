## **Unidade 1 - Práticas Técnicas DevOps**
collapsed:: true
	- <p><span style="color: #d65d0e">DevOps</span> <span style="color: #3588E9">--></span> abordagem baseada em <strong>capacidade técnicas, de processo e culturais</strong> que impulsionam uma maior entrega de software e desempenho organizacional, melhorando a colaboração entre times de desenvolvimento, segurança e qualidade e infraestrutura. É uma <strong style="color: #d79921">mudança cultural</strong> na qual desenvolvedores e engenheiros de operação trabalham juntos durante todo o ciclo de desenvolvimento.</p>
	- <p><span style="color: #3588E9">--></span> A tecnologia é o facilitador da inovação. A tecnologia por si só não irá [ impulsionar a inovação ] <span style="color: #3588E9">--></span> modelo de negócios.</p>
	- <p><span style="color: #d65d0e">DevOps</span> possui três dimensões: <strong style="color: #d79921">cultura</strong>, <strong style="color: #d79921">metodos</strong> e <strong style="color: #d79921">ferramentas</strong>.</p>
	- <p><span style="color: #d65d0e">DevOps</span> busca dividir grandes projetos para entregar uma série contínua de pequenas mudanças que sejam mais gerenciáveis, reduz o risco de grandes projetos. No DevOps, o design da rede é definido pela sua arquitetura e uma infraestrutura efêmera é criada para cada nova implantação.</p>
	- Parte de se tornar uma organização Devops é primeiro se tornar <strong>Agile</strong>, porque Agile é um princípio fundamental do DevOps. As equipes ágeis devem ser equipes pequenas e dedicadas, equipes multifuncionais e equipes auto-organizadas.
	- <p><strong style="color:#689d6a">Pilares do DevOps</span>:</p>
	  collapsed:: true
		- <p><span style="color:#d65d0e">Primeiro Caminho</span> <span style="color: #3588E9">--></span> permite um <strong>fluxo rápido de trabalho</strong> da esquerda para direita de Dev para Ops para o cliente.</p>
		- <p><span style="color:#d65d0e">Segundo Caminho</span> <span style="color: #3588E9">--></span> permite um fluxo rápido e constante de <strong>feedback</strong> da direita para a esquerda em todos os estágios do fluxo de valor.</p>
		- <p><span style="color:#d65d0e">Terceiro Caminho</span> <span style="color: #3588E9">--></span> possibilita a criação de uma <strong>cultura generativa</strong> de alta confiança que apoie uma abordagem dinâmica, disciplinada e científica à experimentação e tomada de riscos.</p>
	- <p><strong style="color:#689d6a">Capacidades Tecnicas Básicas</strong>:</p>
	  collapsed:: true
		- Essas capacidades são habilidades fundamentais que o time de desensolvimento, qualidade, segurança e infraestrutura devem possuir.
		- <p><span style="color: #d79921">Gestão de configuração de código</span> --> estrutura das arvores (braches), politicas de promoçao de replicação de código, politicas de integração a resolução de conflitos. Exemplos de ferramentas: GitLab, Azure Devops, Jenkins.</p>
		- <p><span style="color: #d79921">Automação de testes</span> --> antecipar problemas através de testes automatizados.</p>
		- <p><span style="color: #d79921">Integração Contínua</span> --> prática para construção automatizada de executáveis robustos (builds).</p>
		- <p><span style="color: #d79921">Entrega Contínua</span> --> Prática para a implantação segura de executáveis em ambientes de homologação e produção (releases) </p>
		- <p><span style="color: #d79921">Infraestrutura como Código</span> --> Prática para executar, provisionar ativos de infraestrutura e nuvens através do código.</p>
		- <p><span style="color: #d79921">Conteinerização</span> --> Prática para virtualização de amebientes, servidores e softwares através de contêineres leves</p>
	- <p><strong style="color:#689d6a">Github Actions</span>:</p>
	  collapsed:: true
		- O github actions é uma plataforma CI/CD que permite automatizar a construção, teste e implantação do fluxo de trabalho do GitHub. Permite tratar o pipeline de CI como código. Toda a estrutura do fluxo de trabalho(workflow) é escrita em um arquivo <span style="color:#98971a">yaml</span>.
		- Estrutura do GitHub Acions:
		  collapsed:: true
			- <p>.github
			  |-------------- workflows
			                           |-------------- arquivo.yaml </p>
			-
			- <p><span style="color: #d65d0e">Workflows(Fluxo de trabalho)</span> <span style="color: #3588E9">--></span>  elemento mestre do Github Actions. Um fluxo de trabalho é uma série de procedimentos automatizados representados como Jobs e Steps que o Github Actions executa. Um workflow pode conter um ou mais Jobs.</p>
			- <p><span style="color: #3588E9">--></span> Cada Workflow pussui os seguintes componentes: <span style="color: #d65d0e">Event</span> <span style="color: #3588E9">---></span> <span style="color: #d65d0e">Runner</span> <span style="color: #3588E9">---></span> <span style="color: #d65d0e">Jobs</span> <span style="color: #3588E9">---></span> <span style="color: #d65d0e">Steps</span> <span style="color: #3588E9">---></span> <span style="color: #d65d0e">Actions</span></p>
			- <p><span style="color: #d65d0e">Job</span> <span style="color: #3588E9">--></span> podem conter um conjunto de um ou mais Steps. Cada job pode ser executado de forma independente, ou serem incadeados, condicional. Por padrão, Jobs rodam em paralelo.</p>
			- <p><span style="color: #d65d0e">Runner</span> <span style="color: #3588E9">--></span> ambiente seguro para executar o Job em uma plataforma específica.</p>
			- <p><span style="color: #d65d0e">Steps</span> <span style="color: #3588E9">--></span> tarefas que executam um ouas mais scripts de linha de comando (shell script) ou uma açao (Action). Steps são executados em ordem, mas podem ser condicionais.</p>
			- <p><span style="color: #d65d0e">Actions</span> <span style="color: #3588E9">--></span> pequeno componente de execição que encapsula alguma coisa.</p>
		- <p><span style="color: #3588E9">--></span> Dentro do repositrório pode haver vários workflows, que são ativados através de eventos. Um evento é algo que executa um workflow. Por exempo: publicar o código em uma branch.</p>
		- O Github Action esta vinculado a um repositorio de código do Github.
		- ```yaml
		  name: Primeiro Workflow
		  
		  on:
		  	workflow_dispatch: 
		      
		  jobs:
		  	acao_inicial_job: # identificador do Job
		      
		      	runs-on: ubuntu-latest # runner
		          
		          steps:
		          	- name: Imprime Ola
		                run:	echo "Ola"
		                
		              - name: Imprime Tchau
		                run:	echo "Tchau"
		  ```
	- <p>A engenharia de sistemas DevOps funciona como um fluxo de trabalho de desenvolvimento: Push --> Github --> Docker</p>
	- <p><span style="color: #d65d0e">Pipeline</span> <span style="color: #3588E9">--></span> tecnica que permite que acoes possam ser automatizadas.</p>
	- <p><span style="color: #d65d0e">Pipelines DevOps</span> <span style="color: #3588E9">--></span> mecanismos automatizados para reduzir o <strong>tempo de entrega</strong> de demandas, aumentar o <strong>feedback</strong> entre pessoas e também habilitar <strong>experimentos e inovações</strong>. Pode-se ter múltiplos tipos de pipelines de acordo com o objetivo do papel envolvido.</p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">Integração Contínua (CI)</span>: Build automatizado --> Testes Automatizados --> Entrega no ambiente de testes</p>
		- <p><span style="color: #d65d0e">Entrega Contínua (CD)</span>: Provisiona o ambiente com Docker --> Publica a aplicação em contêiner Docker --> Habilita o contêiner em ambiente de produção.</p>
		- <p><span style="color: #d65d0e">Segurança de Conteineres</span>: Identifica ambientes com vulnerabilidades --> Aplica patch de segurança de forma automatizada --> Gera dados analíticos para time de segurança.</p>
	- <p><span style="color: #d65d0e">DevOps pipeline</span> <span style="color: #3588E9">--></span> Plan - Develop - [ Build - Test ] - Deploy</p>
	- <p> A <strong>automação de builds</strong> é prática essencial para garantir que os executáveis dos produtos sejam gerados de forma consistente, em base diária. Ela externaliza todas as dependências de bibliotecas e configurações feitas dentro de uma IDE para scripts. --> pilar básico para se avançar em direção a fluxos de CI.</p>
	- Automatizar a promoção de builds também deve considerar a promoção de scripts de banco de dados e ate mesmo o transporte de dados de configuração.
	- <p><span style="color: #3588E9">--></span> a prática comum do mercado é que builds devam executar um <strong>conjunto minimo de testes de unidade automatizados (smoke tests)</strong> para estabelecerem confiabilidade mínima ao executável sendo produzido. O teste de unidade tende a ser mais barato, quando um produto estar sendo desenvolvido. O teste de unidade são executados dentro da memória da máquina que esta rodando.</p>
	- <p><span style="color: #d65d0e">smoke test</span> <span style="color: #3588E9">--></span> cria-se um pequeno fragmento de testes que irão testar funções minimas no nível de unidade.</p>
	- <p><strong>Requisitos</strong> para automação de builds: <span style="color: #d79921">acordos entre os times</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Gestão de configuração</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Compilação automatizadas</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Checkins diários de código</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Testes de unidade automatizados</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Suíte abrangente de testes</span> <span style="color: #3588E9">--></span> <span style="color: #d79921">Processo leve de compilação e testes</span>.</p>
	- <p><a href="https://landscape.cncf.io/?group=projects-and-products"><span style="color:#98971a">Portal CNCF</span></a> <span style="color: #3588E9">--></span> portal com uma coleção de ferramentas catalogadas.</p>
	- <p>A <strong>automação de Testes</strong> procura-se garantir a existência de mecanismos automatizados para garantir a conformidade de determinados ativos de software. Deve-se primeiro focar em testes que são mais baratos para serem escritos e executados.</p>
	- <p>Ambiente produtivos podem ter pipelines para proteção de novas publicações <span style="color: #3588E9">--></span> <span style="color: #d65d0e">smoke tests</span>.</p>
	- <p>A <strong>automação de Entregas</strong> é uma prática que busca garantir que o processo de promoção do executável para os ambientes de testes, homologação e produção sejam automatizados e assim tornados consistentes e eficientes. </p>
	- <p><span style="color: #d65d0e">Continuous Delivery(entrega continua)</span> <span style="color: #3588E9">--></span>  realiza a promoção automatizada entre ambientes de desenovlvimento. Exemplos: ambientes de testes integrados ou ambientes de homologação. A ultima etapa antes de entrar em produçõa nunca é automatizada, é realizada por um ser humano.</p>
	- <p><span style="color: #d65d0e">Implantação Contínua(Continuous Deployment)</span> é o processo de promover o executável ao ambiente de produção de maneira automatizada.</p>
	- <p><span style="color: #3588E9">--></span> Toda promoção de ambiente deve incluir processos de verficação da estabilidade.</p>
	- <p><span style="color: #d65d0e">Observabilidade</span> <span style="color: #3588E9">--></span> permite ter mais controle do ambietne que esta em prod e antecipar problemas.</p>
		- Uma boa arquitetura tecnica para geração de registros(logs) é essencial para facilitar a análise de problemas e incidentes em produção.
		- <p><span style="color: #d79921">Monitoramento</span> <span style="color: #3588E9">--></span> instrumentação de um aplicativo para coletar, agregar e analisar registros e métricas para melhoras nossa compreensão do seu comportamento. Incluis observsr o espaço em disco, uso de CPu e o consume de memoria em nós individuos até fazer transaçoes sinttica detalhadas para ver se um sistema ou aplicativo esta correpondendo corretamente e em tempo hábil.</p>
		- <p><span style="color: #d79921">Registro(log)</span> <span style="color: #3588E9">--></span> registros de eventos de negocio. As mensagens de log capturam váriso eventos aontecendo no sistewma, como acoes com falha ou bem sucendidade, informacoes de auditoria ou eventos de sáude. As ferramentas de registro coletam, armazenam e analisam essas mensagem para rastrear relatoriso de erros e dados relacionados.</p>
		- <p><span style="color: #d79921">Rastreamento(Traycing)</span> <span style="color: #3588E9">--></span> permite registrar o caminho de uma solicaçao a medida que ela se move atraves de um sisteasm distribuido.</p>
	- <p><span style="color: #d65d0e">SRE</span> e <span style="color: #d65d0e">DevOps</span> podem ser usados juntos para manter e usar a infraestrutura de computadores.</p>
- ## **Unidade 2 - Práticas Técnicas Avançadas DevOps**
  collapsed:: true
	- <p><span style="color: #d65d0e">Contêineres</span> são mecanismos de virtualização feitos em nível de sistema operacional que permite executar uma aplicação e suas dependências como processos e com recursos isolados que simulam uma máquina virtual. Podem ajudar a garantir rapidez, confibilidade e consistência de implantação, independente do ambiente de implantação.</p>
	- <p><span style="color:#98971a">Docker</span> <span style="color: #3588E9">--></span> é uma tecnologia Open Source que permite criar, executar, e implantar aplicações distribuídas dentro de containers de software.</p>
	  collapsed:: true
		- <p><span style="color:#98971a">dokcerhub</span> <span style="color: #3588E9">--></span> repositório de imagens docker</p>
		- `docker search ubuntu | more` <span style="color: #3588E9">--></span> comando que pesquisa no dockerhub por várias imagens docker com o ubuntu.
		- `docker pull ubuntu` <span style="color: #3588E9">--></span> baixa item de configuração, do ambiente remoto para o ambiente local.
		- `docker images` <span style="color: #3588E9">--></span> lista as imagens.
		- <p><span style="color:#98971a">Dockerfile</span> <span style="color: #3588E9">--></span> local de script na qual o ambiente será preparado</p>
		  collapsed:: true
			- ```Dockerfile
			  # cria a imagem a partir de uma imagem base
			  FROM ubuntu:latest 
			  
			  # Comandos que serão executados dentro da imagem
			  ENV MENSAGEM "Alo Mundo"
			  
			  CMD echo ${MENSAGEM}
			  ```
			- `docker build -t imagem-echo .` <span style="color: #3588E9">--></span> constoi a imagem docker a partir do Dockerfile.
		- `docker images | grep imagem` <span style="color: #3588E9">--></span> lista as imagens filtrando por uma expressão regular
		- `docker run imagem-echo` <span style="color: #3588E9">--></span> executa a imagem
	- <p>O <span style="color:#98971a">docker compose</span> prepara de uma única vez todo um conjunto de imagens, basicamente uma topologia inteira é preparada em um único arquivo.</p>
	- <p>O papel do conteiner de banco de dados é utilizar um <span style="color: #d65d0e">volume</span> <span style="color: #3588E9">--></span> diretório externo, tipicamente organizado em um file system que terá o banco de dados.</p>
	- O comando `docker-compose up --build` irá construir o ambiente e subir o conteiner.
	- <p><span style="color: #d65d0e">Orquestração de Contêineres</span> é basicamente administrar uma grande quantidade de contêineres através de ferramentas como <span style="color:#98971a">Kubernetes</span>, <span style="color:#98971a">Docker Swarm</span> ou <span style="color:#98971a">Open Shift</span>. Um administrador de contêineres pode detectar um determinado problema dentro de um cluster e usar a prática <span style="color:#689d6a">Configuração de Estado Desejado (Desired State Configuration)</span>. O <span style="color:#689d6a">DSE</span> é uma regra que informa ao administrador de contêineres o número desejado de contêineres que uma máquina deve ter.</p>
	- <p>O <span style="color:#98971a">Kubernetes</span> criado pela Google, se tornou um padrão de mercado.</p>
	- Orquestradores de Contêineres administram de forma integrada todo o conjunto de contêineres, monitoram, geram estatística, mantêm o estado de configuração desejado, implementam o conceito de computação elástica.
	- <p><strong style="color:#689d6a">Docker Swarm</strong>:</p>
	  collapsed:: true
		- <p>O subcomando swarm <span style="color: #3588E9">--></span> permite gerenciar um grupo de contêineres.</p>
		- <p><span style="color:#689d6a">swarm</span> <span style="color: #3588E9">--></span> um conjunto de várias máquinas que terão a capacidade de rodar múltiplos contêineres.</p>
		- > `docker swarm init` <span style="color: #3588E9">--></span> prepara o swarm
		  >
		  > `docker swarm join` <span style="color: #3588E9">--></span> adiciona a máquina ao enxame
		- Após preprar o enxame deve-se criar um serviço. Um serviço permite estanciar um conjunto de conteineres que irao operar dentro de um determinado enxame.
		- <p><span style="color: #3588E9">--></span> Um <span style="color: #d65d0e">serviço</span> é uma forma de rodar um conjunto de contêineres de uma forma integrada em um conjunto de uma ou mais máquinas físicas dentro de um determinado enxame.</p>
		- > `docker service` <span style="color: #3588E9">--></span> permite fazer o gerencimento de um serviço
		  >
		  > `docker service create --name enxame-meuapp --replicas 3 --publish 8080:8080 meu-app`
		  >
		  > `docker service scale` <span style="color: #3588E9">--></span> permite escalar o serviço
		  > 
		  > `docker service scale enxame-meu-app=5`
		  >
		  > `docker service ls` <span style="color: #3588E9">--></span> exibe detalhes do serviço
		- <p><span style="color: #3588E9">--></span> as replicas são alocadas dinamicamente no conjunto de máquinas físicas (balanceamento de carga).</p>
		- <p><span style="color:#689d6a">round robin</span> <span style="color: #3588E9">--></span> algoritmo de balanceamento de carga</p>
	- <p><span style="color: #d65d0e">Infraestrutura como Código (IaC)</span> é uma abordagem de DevOps e gerenciamento de infraestrutura que trata a infraestrutura de computação como código de software.</p>
	- <p><strong style="color:#689d6a">Terraform</strong>:</p>
	  collapsed:: true
		- <p><span style="color:#98971a">Terraform</span> é uma ferramenta de Infraestrutura como código (IaC) criada pela Hashicorp que permite automatizar e gerenciar através de código (provisionar), Infraestrutura de Data Centers, as plataformas e o serviços que rodam nessas plataformas. Obs: O terraform é uma linguagem declarativa.</p>
		- A estrutura básica de um arquivo de terraform é composta por providers e resources (recursos)
		  collapsed:: true
			- <p>Em uma configuração simples o arquivo <span style="color:#98971a">main.tf</span> irá conter todo conjunto de configurações para o módulo do terraform.</p>
			- ```terraform
			  terraform {
			      required_providers {
			          docker = {
			              source = "kreuwerker/docker"
			          }
			      }
			      
			  }
			  
			  provider "docker" {
			      host = "unix:///Users/guilherme/.docker/run/docker.sock"
			  }
			  
			  resource "docker_image" "nginx" {
			      name = "nginx:latest"
			  }
			  
			  resource "docker_container" "nginx1" {
			      image = docker_image.nginx.image_id
			      name = "nginx1"
			      ports {
			          internal = 80
			          external = 8081
			      }
			  }
			  
			  resource "docker_container" "nginx2" {
			      image = docker_image.nginx.image_id
			      name = "nginx2"
			      ports {
			          internal = 80
			          external = 8085
			      }
			  }
			  ```
			- <p><span style="color:#98971a">Módulo (module)</span> <span style="color: #3588E9">--></span> diretório que irá conter uma mais configurações (.tf), é basicamente um contêiner para múltiplos recursos que são utilizados em conjunto.</p>
			- <p><span style="color:#98971a">Providers</span> <span style="color: #3588E9">--></span> plugins que o Terraform utiliza para criar e gerenciar recursos em uma infraestrutura específica.</p>
			- <p><span style="color:#98971a">Resources</span> <span style="color: #3588E9">--></span> elemento mais importante da configuração do Terraform. Um bloco de recursos declara um recurso de um determinado tipo, com um nome local. No caso de uma infra estrutura de núvem na AWS, o recurso representa um serviço fornecido pela AWS como por exemplo, uma instância EC2.</p>
		- <p><strong>Workflow</strong> do <span style="color:#98971a">Terraform</span>: <strong style="color: #d79921">Write</strong> <span style="color: #3588E9">---></span> <strong style="color: #d79921">Plan</strong> <span style="color: #3588E9">---></span> <strong style="color: #d79921">Apply</strong></p>
		  collapsed:: true
			- `terraform init` <span style="color: #3588E9">--></span> inicializa o módulo root do terraform
			- `terraform plan` <span style="color: #3588E9">--></span> compara o estado atual como estado que o arquivo esta declarando, ele calcula a diferença em termos de elementos a serem adicionados, removidos e destruidos
			- `terraform apply` <span style="color: #3588E9">--></span> aplica a configuração do terraform
			- `terraform destroy` <span style="color: #3588E9">--></span> detecta toda a topologia e redefine o ambiente para o ponto de partida; destrói todos recursos.
		- `terraform plan -out = tfplan` <span style="color: #3588E9">--></span> salva o plan gerado em um determinado arquivo
		- <p><span style="color: #3588E9">--></span> O terraform permite o versionamento da infraestrutura.</p>
	- <p><span style="color: #d65d0e">Engenharia do caos</span> é uma prática avançada para experimentar um sistema a fim de construtir confiança na capacidade do sistema de suportar condições turbulentar na produção.</p>
	- <p>A Engenharia do Caos busca expor as fraquezas do ambiente antes que elas se manifestem em um determino horário que os engenheiros não estejam trabalhando. Essa abordagem visa estressar o ambiente para aprender como ele se comporta, com o intuito de tornar a infraestrutura robusta. Exemplo de ferramenta: Simian Army --> ferramenta da Netflix.</p>
	- <p><span style="color: #d65d0e">Estressor</span> é algo que se deseja observar. Exemplos: Aumento de carga de um processor, terminar um contêiner, etc.</p>
	- <p><strong>Etapas</strong> de Engenharia do Caos: <span style="color: #d79921">definir o "estádo estavel"</span> <span style="color: #3588E9">---></span> <span style="color: #d79921">testa no grupo de controle</span> <span style="color: #3588E9">---></span> <span style="color: #d79921">introduz estressores no ambiente</span> <span style="color: #3588E9">---></span> <span style="color: #d79921">comparar o estado estável entre o grupo controle e o grupo experimental</span>.</p>
	- <p>Portal <a href="https://principlesofchaos.org/"><span style="color:#98971a">princinpleofchaos</span></a></p>
	- <p><span style="color: #d65d0e">DevSecOps</span> <span style="color: #3588E9">--></span> movimento que busca aproximar as areas de segurança, de operação e de desenvolvimento. Dessa forma as práticas DevOps como uso pipelines automatizadas são incorpordas pelo time de segurança. Exemplo de práticas de segurança: verificação automatizada da segurança do código após commits, verificação de segurança automatizada de ambiente.</p>
	- <p><span style="color: #d65d0e">Segurança por desenho (Security by design)</span> <span style="color: #3588E9">--></span> signifca que o problema de segurança é de toda a organização, as boas práticas de segurança são incorporadas para todo o ciclo de desensolvimento.</p>
- ## **Unidade 3 - Capacidades de Processo e Culturais em DevOps**
  collapsed:: true
	- DevOps além de involver práticas técnicas, também envolve práticas ligadas a processos e a asectos culturais.
	- <p>O Instituto DORA (Instituto de Avaliação e Pesquisa em DevOps) documentou uma série de <span style="color: #d65d0e">Práticas de Processo</span>:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Feedback do cliente</span> <span style="color: #3588E9">--></span> fundamental para acionar um conceito de ciclo de feedback (aspecto ligado ao produto ou perspectiva arquitetural).</p>
		- <p><span style="color: #d79921">Monitoramento de sistemas para informar decisões de negócios</span> <span style="color: #3588E9">--></span> busca ativar Observabilidade.</p>
		- <p><span style="color: #d79921">Notificação proativa de falhas</span> <span style="color: #3588E9">--></span> procura evitar situações anormais acontecendo em ambiente produtivo. Implica em definir limites e regras de acionamento, assim como, definir como alarmes serão trabalhados em toda a cadeia de pessoas envolvidas na organização</p>
		- <p><span style="color: #d79921">Simplificação da aprovação de mudanças</span> <span style="color: #3588E9">--></span>  a ideia é criar conhecimento e trabalho compartilhado entre os participantes através do conceito de Revisão por Pares. Envolve que as pessoas estejam revisando em tempo real artefatos de código gerados por outros colegas entre equipes (exemplo: Git Pull Request).</p>
		- <p><span style="color: #d79921">Experimentação em Equipe</span> <span style="color: #3588E9">--></span> equipes devem ter autonomia dentro de parametros apropriados realizar experimentações de tecnologias, práticas técnicas e outros elementos que permitem produzir com mais velocidade e robustez (cultura generativa).</p>
		- <p><span style="color: #d79921"> Visibilidade do trabalho no fluxo de valor</span> <span style="color: #3588E9">--></span> práticas de gestão que permitem que todo o fluxo de valor, do conceito inicial até o resultado de negócio estejam claramente visíveis (exemplo: sistema Kanbam).</p>
		- <p><span style="color: #d79921">Gestão visual</span> <span style="color: #3588E9">--></span> Utilização de dashboards que exibem por exemplo, a qualidade dos commits, a qualidade de revisão de código, os indicadores de sistemas em produção.</p>
		- <p><span style="color: #d79921">Limites de trabalhos em processo (WIP)</span> <span style="color: #3588E9">--></span> prática que procura limitar a quantidade de coisas que estão sendo trabalhadas e que permitem que as pessoas concentrem em um pequeno número de tarefas de alta prioridade.</p>
		- <p><span style="color: #d79921">Trabalhos em pequenos lotes</span> <span style="color: #3588E9">--></span> evitar demandas muito grandes que levarão semanas ou meses até tocar o ambiente de produção. Exemplo: quebrar um épico ou feature em pequenos cenários.</p>
	- <p><span style="color: #3588E9">--></span> Cultura são os comportamentos que são praticados constantemente dentro de uma organização.</p>
	- <p>As 4 <span style="color: #d65d0e">Grandes Capacidades Culturais</span> pelo Institudo DORA:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Cultura organizacional generativa</span> <span style="color: #3588E9">--></span> cultura na qual abilita o ambiente onde as pessoas possam aprender e experimentar, e o erro deve ser tratado sempre como uma oportunidade de crescimento (o que foi aprendido com uma falha). O erro é tratado como uma curiosidade positiva.</p>
		- <p><span style="color: #d79921">Satisfação no Trabalho</span> <span style="color: #3588E9">--></span> garantir que as equipes estejam satisfeitas com o que estão fazendo.</p>
		- <p><span style="color: #d79921">Cultura de Aprendizado</span> <span style="color: #3588E9">--></span> sistema organizado que permite que pessoas explorem e aprendem novas tecnologias.</p>
		- <p><span style="color: #d79921">Liderança Transformacional</span> <span style="color: #3588E9">--></span> liderança que irão criar um sistema de trabalho que permite que as mudanças possam ocorrer de forma apropriada.</p>
	- <p>As 4 <span style="color: #d65d0e">Métricas</span> pelo Instituto DORA:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Tempo de Entrega para Mudanças</span> (Lead Time for Changes) <span style="color: #3588E9">--></span> mede o tempo que uma equipe aceitou uma determianda solicitação (demanda) e o momento que o código esta operando em produção. </p>
		- <p><span style="color: #d79921">Frequência de Implantação</span> (Deployment Frequency) <span style="color: #3588E9">--></span> o quão frequente se é na implantação.</p>
		- <p><span style="color: #d79921">Tempo Médio para Recuperação</span> (Mean Time for Recovery, MTTR) <span style="color: #3588E9">--></span> o quão bem se recupera de uma falha.</p>
		- <p><span style="color: #d79921">Taxa de Falha de Mudanças</span> (Change Failure Rate) <span style="color: #3588E9">--></span> regula o tempo de entrega e frequência.</p>
		- <p><span style="color: #3588E9">--></span> o que se busca com todas as métricas é reduzir o tempo de entrega, embora elas devam ser trabalhadas em conjunto.</p>
	- <p><strong>Valor de negócio</strong> <span style="color: #3588E9">--></span> efeito da utilização da tecnologia.</p>
	- As ferramentas devem ser implantadas para resolverem um problema na organização.
	- <p><span style="color: #d65d0e">Implantanção Canário</span> <span style="color: #3588E9">--></span> teste de uma nova funcionalidade de infraestrutura em um ambiente Canário (número limitado de uma população).</p>
	- <p><span style="color: #d65d0e">Desenvolvimento Baseado em Tronco</span> (Trunk Base Development) <span style="color: #3588E9">--></span> prática muito alinhada à entrega contínua, que implica uma disciplina forte de revisões de código.</p>
- ## **Unidade 4 - Maturidade de Práticas DevOps**
  collapsed:: true
	- <p><span style="color: #d65d0e">Escala de Maturidade DevOps</span>:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Nivel 1 - Inicial</span> (ou Inconsciente): Não há consciência da aplicação de uma determinada prática de DevOps, assim como não há um processo definido.</p>
		- <p><span style="color: #d79921">Nivel 2 - Consciente</span>: Reconhece que há uma prática de DevOps, já reconhece o que é Iac, mas não se sabe trabalhar com as ferramentas. É um nível marcado pela experimentação de aprendizado. O processo esta emergindo, mas não é muito bem definido.</p>
		- <p><span style="color: #d79921">Nivel 3 - Gerenciado</span>: Nesse nível há o reconhecimento das práticas de DevOps. Várias experimentações já foram realizadas e já possui uma suíte de ferramentas mas bem consolidadas. Entretanto, a qualidade ainda é inconsistente, pois ainda há falhas na execução de um processo (equipe ainda está aprendendo a como operar no novo ambiente).</p>
		- <p><span style="color: #d79921">Nivel 4 - Quantitativamente Gerenciado</span>: Há um reconhecimento pleno das práticas de DevOps, o processo é bem definido assim como o conjunto de ferramentas. Os resultado são claros e se consegue demonstrar o efeito em indicadores.</p>
		- <p><span style="color: #3588E9">--></span> Para se evoluir na escala de maturidade não há caminho linear (campo do complexo), na verdade se parte do lugar atual e vai avançado reliazando avaliações de ajuste (o quão se esta operando), no que resulta em práticas de melhorias (experimentos são realizados). O processo esta em evolução contínua.</p>
		- <p><span style="color: #d65d0e">mudanças evolucionárias</span> <span style="color: #3588E9">--></span> contexto de gestão de mudanças que opera no campo do complexo.</p>
		- <p><span style="color: #3588E9">--></span> a avaliação da maturidade é sempre realizada dentro de um contexto e para que a avaliação seja feita, deve-se observar (elementos concretos) e coletar evidências.</p>
	- <p><span style="color: #d65d0e">Maturidade de Automação de Builds</span>:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Nivel 1 - Inicial</span>: Não há consciência da automação de builds, os processos são manuais, não há automação de testes e todo o processo de compilação de código esta amarrado a uma IDE.</p>
		- <p><span style="color: #d79921">Nivel 2 - Consciente</span>:  Há consciência sobre o processo de automação de builds, algumas ferramentas estão sendo testadas. Porém, ainda não um processo de automação de builds definido. Não se depende mais de IDEs para compilar código e automação des testes começa a ser inserida.</p>
		- <p><span style="color: #d79921">Nivel 3 - Gerenciado</span>: As ferramentas para automação de builds já foram consolidadas, mas ainda não se tem resultados plenamente efetivos. Vários processos técnicos podem emergir.</p>
		- <p><span style="color: #d79921">Nivel 4 - Quantitativamente Gerenciado</span>: Nível no qual a Integração Contínua foi implementada, é possivel demonstrar resultados consistentes.</p>
		- <p><span style="color: #d65d0e">automação de builds</span> <span style="color: #3588E9">--></span> é gerar um executável robusto, ou seja, o executável deve passar pelo escrutínio de um conjunto de testes automatizados.</p>
	- <p><span style="color: #d65d0e">Maturidade de Automação de Entregas</span>:</p>
	  collapsed:: true
		- <p>automação de entregas <span style="color: #3588E9">--></span> processo de promoção de executáveis (builds).</p>
		- o papel da automação de entregas é mover o executável entre ambientes.
		- <p><span style="color: #3588E9">--></span> se o processo de automação de entregas é fluido, opera sem transtorno e pode ser executado com cinfiabilidade de uma forma rápida dentro dos ambientes de homologação e produção, significa que se tem maturidade de automação de entregas.</p>
		- <p><span style="color: #d79921">Nivel 1 - Inicial</span>: O processo de builds é manual; uso de scripts rudimentares; manipulação de banco de dados tender a ser manual; problemas em produção (instabilidades).</p>
		- <p><span style="color: #d79921">Nivel 2 - Consciente</span>: Processos começam a ser automatizados; ferramentas como Azure Pipelines começam a ser experimentadas assim como docker e orquestração de contêineres.</p>
		- <p><span style="color: #d79921">Nivel 3 - Gerenciado</span>: Os processos se integram a normativas (como por exemplo ITIL) e outros processos que vem do ambiente de infra estrutura, mas os resultados ainda não são plenamente efetivos.</p>
		- <p><span style="color: #d79921">Nivel 4 - Quantitivamente Gerenciado</span>: Há CD (Implantação Contínua) e uso pleno de tecnologias que ajudaram a estabelecer o processo que aconteceram do nível anterior; a qualidade é consistente.</p>
	- <p><span style="color: #d65d0e">Maturidade de Automação de Ambientes e IaC</span>:</p>
	  collapsed:: true
		- <p><span style="color: #d79921">Nivel 1 - Inicial</span>: O provisionamento é feito de forma manual; não há uso de contêineres.</p>
		- <p><span style="color: #d79921">Nivel 2 - Consciente</span>: Ferramentas como Docker, Ansible, Terraform começam a ser experimentadas; pequenos scripts de automação começam a ser experimentados.</p>
		- <p><span style="color: #d79921">Nivel 3 - Gerenciado</span>: A suíte de ferramentas é consolidada e processo é bem definido. Mas ainda não se tem instrumentação do processo nem medições dos seus benefícios econômicos.</p>
		- <p><span style="color: #d79921">Nivel 4 - Quantitivamente Gerenciado</span>: Automação da infraestrutura é em larga; o uso das ferramentas estão largamente disseminado; práticas avançadas como Engenharia do Caos são experimentadas.</p>
	- <p><span style="color: #3588E9">--></span> <strong style="color: #d79921">A transformação DevOps não deve ser tratado como um projeto, pois é uma jornada continuada</strong> (experimentação --> método científico).</p>
	- <p>Deve-se ter <strong>boas práticas</strong> que possam ser disseminadas à medida que elas forem acontecendo e emergindo dentro de times. Frameworks como o OKRS (condição alvo de curto prazo) podem ajudar a definir <strong>metas claras</strong>. Entretanto, a dinâmica básica da trasnformação é comum a todos os frameworks.</p>
	- <p>Abordagem Sistemastematizada <span style="color: #3588E9">--></span> <span style="color: #d65d0e">Modelo Toyata Kata</span> (ciclos continuados de experimentação).</p>
	- <p><span style="color: #d65d0e">estressor de melhorias</span> <span style="color: #3588E9">--></span> tornar a capacidade do sistemas de trabalho mais forte</p>
	- <p><span style="color: #d65d0e">OKRs</span> <span style="color: #3588E9">--></span> estabelecem um ciclo curto e partem de um objetivo qualitativo.</p>
	- <p><span style="color: #3588E9">--></span> <strong style="color: #d79921">trabalhar com ciclos de curto prazo e identificar o nível de maturidade DevOps</strong>.</p>
	- <p><span style="color: #d65d0e">Mapas de calor</span> auxiliam a identificar o nível de maturidade de práticas DevOps de vários times.</p>
	- <p>A <em>verificação rápida de métricas</em> <span style="color: #d65d0e">DORA</span> pode ajudar a avaliar a condição atual da organização.</p>
	- <p>Realizar ciclos de experimentação através de <span style="color:#689d6a">Provas de Conceito</span> (POC), práticas técnicas e sociológicas.</p>
	- <p>método <span style="color: #d65d0e">OODA</span> <span style="color: #3588E9">--></span> abordagem inspirada no PDCA, ajuda mais no processo mental de melhoria.</p>
	- <p><span style="color: #3588E9">--></span> Realizar perguntar diárias como: <li>"Qual é a nossa condição alvo?"</li><li>"O que estamos tentando alcançar?"</li><li>"Quais obstáculos estamos enfrentando?"</li><li>"Quais são os próximos passos?"</li></p>
	- <p><span style="color: #3588E9">--></span> <strong style="color: #d79921">Adapatação é parte integral dentro de uma jornada DevOps</strong>.</p>
	- <p>As equipes devem definir suas próprias metas, e utilizar os erros como estratégia de aprendizagem e amadurecimento.</p>
	- <p>Ferramenta <a href="https://dora.dev/quickcheck/"><span style="color:#98971a">DoraDev</span></a> para verificar o nível da maturidade DevOps.</p>
	- <p><strong style="color:#689d6a">FinOps</strong></p>
	  collapsed:: true
		- Disciplina Complementar ao mundo DevOps.
		- <p><span style="color: #d65d0e">FinOps</span> é uma junção de "Financial" e "(Dev)Ops" enfatizando a comunicação e colaboração entre times de negócios e engenharia.</p>
		- FinOps tem a ver como criar oportunidades financeiras a partir de um modelo escalável e variável de núvem.
		- Também é prática cultural, mas que busca aumentar o valor de negócio com oportunidades ligadas a núvens e tecnologias de DevOps.
		- A núvem passa ser uma responsblidade de todo mundo. Um desenvolvedor, ou um analista de qualidade, tem que começar a ter entendimento do efeito de uma decisão técnica no custo de núvem.
		- A questão fincanceira passa a ser compartilhada como uma oportunidade e também como uma responsabilidade compartilhada.
		- A ideia do FinOps é combinar os vários elementos que estão conectados a uma compreensão dos produtos de núvem a entendimento do desempenho de benchmark das aplicações e como isso esta se refletindo nos custos fincanceiros de uma forma geral.
		- <p>A jornada FinOps enolve uma conjunto de etapas: <li><span style="color: #d79921">planjemento</span> <span style="color: #3588E9">--></span> como exercitar de forma responsável a utilização dos recursos de núvem (oportunidades fincanceiras e racionalização de custos)</li><li><span style="color: #d79921">socialização</span> <span style="color: #3588E9">--></span> impulsinar investimentos, trabalhar requisitos de ferramentas, disseminar o uso de calculadoras fincanceiras de núvem</li><li><span style="color: #d79921">preparação</span> <span style="color: #3588E9">--></span> criação de indicadores para monitorar a jornada e busca disseminar e implantar as ferramentas que irão auxiliar a criar oportunidades variáveis com modelos de núvem</li><li><span style="color: #d79921">inicio</span> <span style="color: #3588E9">--></span> executar plano de comunicação e gestão de mudanças</li><li><span style="color: #d79921">execução</span> <span style="color: #3588E9">--></span> evolução permanente das ferramentas tecnicas e financeiras</li></p>
		- <p><a href="https://calculator.aws/#/"><span style="color:#98971a">Calculadora AWS</span></a> <span style="color: #3588E9">--></span> permitar orçar um conjunto de serviços das AWS.</p>
		- <p><a href="https://www.cloudcraft.co/"><span style="color:#98971a">Cloudcraft</span></a> <span style="color: #3588E9">--></span> ferramenta para realizar desenhos de topologia de núvem.</p>
		- <p>Orçamentação <span style="color: #3588E9">--></span> prática do FinOps</p>