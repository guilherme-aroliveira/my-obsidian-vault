## **Unidade 1 - Visão Geral dos Testes de Software**
collapsed:: true
	- <p><strong style="color: #d79921">Erro</strong> <span style="color: #3588E9">--></span> ocasionado por alguma pessoa (Analista, Arquiteto, Desenvolvedor). Exemplo: sintaxe incorreta utilizada no código por um desenvolvedor.</p>
	- Erro pode gerar ou não um defeito. Entretanto, o defeito é gerado a partir de um erro.
	- <p><strong style="color: #d79921">Erro de especificação</strong> <span style="color: #3588E9">--></span> erro de formalidade, não impacta diretamente a aplicação.</p>
	- A pluraridade de testes, envolve níveis de testes, tipos de testes e técnicas de testes (Quando, O que e Como testar).
	- <p><strong style="color:#d79921">"V" dos Testes</strong> <span style="color: #3588E9">--></span> níveis de testes, que vai do micro ao nível macro.</p>
	  id:: 663ecaac-3946-4116-8e26-d7c08549433c
	  collapsed:: true
		- <p><strong style="color: #98971a">Teste Unitário:</strong> visa testar a menor unidade do código, como uma classe por exemplo.</p>
		  logseq.order-list-type:: number
		- <p><strong style="color: #98971a">Teste de Integração:</strong> realiza um teste integrado de todas as unidades feitas em um teste unitário.</p>
		  logseq.order-list-type:: number
		- <p><strong style="color: #98971a">Teste de Sistema:</strong> voltado para a questão da aplicação. Possui os testes funcionais (funcionalidade do sistema) e os não funcionais. Um teste não funcional abrange a questão da segurança, a questão do desempenho, usuabilidade e assecibilidade.</p>
		  logseq.order-list-type:: number
		- <p><strong style="color: #98971a">Teste de Aceite:</strong> garante que o requisito de negócio foi atendido.</p>
		  logseq.order-list-type:: number
	- <p><strong style="color:#689d6a">Tecnicas de testes</strong></p>
	  collapsed:: true
		- <p><strong style="color: #d79921">CaixaPreta</strong>: teste baseado na especificação, na funcionalidade/documentação do sistema<ul style="list-style-type:disc"><li>Se verifica na "<strong style="color: #b16286">interface</strong>" se o sistema obedece o que foi definido na sua especificação.</li><li>A tecnica de <strong style="color: #b16286">CaixaPreta</strong> aumenta a qualidade dos testes.</li><li>Caso o sistema não possui especificação, aborda-se o <strong style="color: #d79921">teste exploratório</strong> <span style="color: #3588E9">--></span> não testa a exceção.</li><li><span style="color: #3588E9">--></span> A especificação também deve abordar situações de exceção.</li></ul></p>
		- <p><strong style="color: #d79921">CaixaBranca</strong>: conhecido também por tecnica baseada em teste estrutural<ul style="list-style-type:disc"><li>teste baseado no código</li><li>não precisa do sistema estar funcionando</li><li>pode ser de forma manual ou de forma automatizada</li><li>Exemplo: teste unitário</li></ul></p>
	- <p><span style="color: #3588E9">--></span> O teste <strong style="color: #b16286">não</strong> é uma fase do ciclo do desenvolvimento e sim uma parte de <strong style="color: #b16286">todas</strong> as fases.</p>
	- <p><span style="color: #d65d0e">Regra 10 Myers</span> <span style="color: #3588E9">--></span> Para cada fase que o teste não é executado corretamente, o custo aumenta ao longo de cada fase.</p> > <p><strong style="color: #C6554F">Nota:</strong> Deve-se entender bastante o conceito de teste.</p>
	- <p><strong style="color: #d79921">Garantia de Qualidade</strong> <span style="color: #3588E9">--></span> relacionado a qualidade dos processos</p>
	- <p><strong style="color: #d79921">Controle de Qualidade</strong> <span style="color: #3588E9">--></span> relacionado a qualidade dos productos de software</p>
	- <p><span style="color: #3588E9">--></span> O teste de software esta abordando a qualidade do produto.</p>
	- <p><strong style="color: #98971a">Garantia da Qualidade</strong> <strong style="color:#689d6a">+ Controle de Qualidade</strong> <strong style="color: #b16286">= Qualidade do Sofware</strong></p> > <p><strong style="color: #d79921">Qualidade de Software</strong> é um <strong style="color: #b16286">processo sistemático</strong> que focaliza todas as etapas e artefatos produzidos com o objetivo de garantir a conformidade de processos e produtos, prevenindo e eliminando defeitos.</p>
	- <p>Exemplos de <strong style="color: #d79921">Modelos de Maturidade</strong>:</p>
	- <p><span style="color: #3588E9">--></span> Não focar apenas na qualidade da aplicação, mas focar na qualidade do negócio.</p> > <p>Nota: Uma falha no sistema envolve a perda de um cliente/negócio</p>
	- Para obter a qualidade dos serviços digitais: automação sem atrito, detectar falhas preventivamente (modelo proativo), implantação de uma área de qualidade (centro de competência), evoluir para um centro de excelência (mudança de mentalidade), criação chapters, investir em plataformas de gerenciamento inteligente de ciclo de vida de software.
- ## **Unidade 2 - Verificação, Validação e Inspeção**
  collapsed:: true
	- <p><strong style="color: #689d6a">Verificação e Validação</strong> <span style="color: #3588E9">--></span> asseguram que o softwarre cumpra as suas especificacoes e atenda as necessidades do usuário</p>
	  collapsed:: true
		- o teste é principal tecnica do V&V
		- devem ocorrer durante e depos do desenvolvimento (processo retroalimentado)
		- o modelo V ilusta as ativades de teste durante o desenvolvimento
		- Verificação estatica --> teste estatico; não necessárioa haver um sistema em exeucção
		- Validação dinamico --> teste dinamico; o sofwatre etsa pronto.
		- objetivos: demonstar que softwarre atende a sua especificacao (construção certa?)  e demontrar que o sofwate atende a necessidade do cliente (producto certo?); identificacao de falahas do sistema e assegudar que o sistema é ou nãoutilizável em situação
	- Premissas de Teste : pode revelar a presença de erros e não a ausencia; teste bem suceido é aquele que descobre um ou mais defeitos, erros ou falhas; única tectica de validação para rwequsitos não funcionais; deve ser usado em conjunto com a verificação estátia para cobertura total das atividade de V&V. Fica claro qual que o escopo que se pretende atingir, sem definir o papael do teste pode-se confondundir dentro do processo e pode não gerar os resultados.
	- <p><span style="color: #d65d0e">Confiabilidade</span> <span style="color: #3588E9">--></span> depende do proposito do sistema (função), expectativas do usuário e do ambiente do mercado</p>
	- Enquanto testar se preocupa em estabelecer defietos no software, depurar é a atividade pela qual a preocupação é localizar e remover os defeitos no codigo. Depurar envolve a formulação de uma hipotese sobre o comportamento do programa e testa-lá para encontrar o erro do sistema.
	- <p><span style="color: #d65d0e">Tecnica particação de equivalencia</span> <span style="color: #3588E9">--></span> as falhas de software ocorre nos pontos de interseção entre os grupos. Busca especificar dentro do primeiro grupo um caso, do segundo outro case, e do terceiro grupo um outro caso. Define tres grupos, tres cenários de testes.</p>
	- <p><strong style="color: #689d6a">Plano de Teste</strong></p>
	  collapsed:: true
		- Inicio no começo do process ode desenvolvimento
		- Defini o equilibrio entre abordagens estáticas e dinamicas
		- Estabelece os padrões paea o processo de teste (abordagem, tecnicas, ferramentas)
		- Itens/Estrutura (pode ser melhorada) --> [Processo --- Rastreabilidade dos requisitos --- Itens a ser testados -- Cronograma de testes -- Procedimentos de registro de testes -- Requisitos de harware e software --- definir as restições].
	- <p><strong style="color: #689d6a">Teste Alfa e Beta</strong></p>
	  collapsed:: true
		- <p><span style="color: #d65d0e">teste alfa</span> <span style="color: #3588E9">--></span> Teste interno; teste de aceitação que ocorre antes de o sistema ser entregue para o cliente. É feito até que o cliente aceite que o sistema seja entregue; ambiente de staging (homologação)</p>
		- <p><span style="color: #d65d0e">teste beta</span> <span style="color: #3588E9">--></span> entrega o sistema a um conjunto de usuário (potenciais clientes). usurios reportam os erros entrados aos devs</p>
	- <p><strong style="color: #689d6a">Inspeção de Software/programas</strong> <span style="color: #3588E9">--></span> processo de analisar o código fonte sem executá-lo.</p>
	  collapsed:: true
		- É uma tecnica complementar e essencial para a qualidade de software
		- O código é sistematicamente checado por um outra pessoa da equipe
		- Em uma unica inspeção vários problemas podem ser identificados
		- Reutilização do conhecimento
		- Podem verificar conformidades em uma especificação
		- Não pode verificar as caracterias não funcionais (ex: desempenho, usuabilidade)
		- Objetivo: detectar erros!!
		- <p><strong style="color: #d79921">Pré condiçoes</strong></p>
			- uma especificação é necessário esta disponivel
			- os mebros da equipe de inspeção devem estar familiarizados com os padroes da organização
			- O código sintaticamente correto deve estar disponivel
			- Uma lista de erros deve estar preparada
		- <p><strong style="color: #d79921">Especificação formal e inspeções</strong></p>
			- O modelo baseado em estados é a especificação, e o processo de inspeção checa o programa com relação a esse modelo
			- A abordagem utilizada para o desenvolvimento tem como base transformações bem definidas
			- Argumentos matemáticos (não provas) são usados para aumentar a confiança no processo de inspeção
		- <p><strong style="color: #d79921">Inspeção automatizada</strong></p>
			- Ferramentas:
				- Sonarqube --> plataforma de códig aberto, para inspeção contínua de qualidade de código, e realiza revisão de forma automática.
				- code climate --> plataforma web para code review
				- Codacy --> automatiza code review, monitora a qualidade
			- code smell
	- <p><strong style="color: #689d6a">Analise estática automatizada</strong></p>
		- os analizadores estáticos são ferramentas de software
		- percorre todo o código, para descobrir potenciais condições erradas
		- É um complemento, porém não substitui as inspeções.
	- <p><span style="color: #3588E9">--></span> <span style="color: #d65d0e">Complexidade ciclomática</span></p>
- ## **Unidade 3 - Níveis de Testes**
  collapsed:: true
	- <p><strong style="color: #689d6a">Teste unitário</strong> <span style="color: #3588E9">--></span> fase onde <strong style="color: #b16286">cada unidade do sistema é testada individualmente</strong>, é o primeiro teste a ser executado. É reponsável por examinar o comportamento do código sobre as mais variadas condições.</p>
	  collapsed:: true
		- quando isolado, não pode conter dependencias externas
		- <p>não se guarda em estados (stateless) <span style="color: #3588E9">--></span> todos recursos utilizados devem ser destruídos</p>
		- testa apenas uma unica unidade
		- permitem uma maior cobertuda do teste
		- <p>prevensão da regressão (problema que volta a ocorrer)</p> > Um dos maiores problemas relacionados a Qualidade de Software é regressão de defeitos.
		- <p>incentiva o <span style="color: #d65d0e">refactoring</span> (revisão de código) <span style="color: #3588E9">--></span> é uma forma de otimizar e atingir a melhor qualidade do código</p>
	- <p><strong style="color: #689d6a">Teste de integração</strong> <span style="color: #3588E9">--></span> testa as unidades que foram testatadas isoladas de forma integrada. </p>
	  collapsed:: true
		- a interface e a comunicação entre as unidades são testadas
		- <p>deve ser feita de forma incremental, as unidades devem ser integradas em pequenos segmentos <span style="color: #3588E9">--></span> utilizar cenários em que as unidades sejam relacionadas.</p>
		- deve ser executado por alguém que conheça teste de integração
		- definir o critério de software e hardware (ambiente)
		- <p>recomendado usar Mocks (unidade falsa) e stubs (unidade mínima)</p> > Uso de emuladores/simuladores (próprio código) para que possa ser uma imitação ou unidades falsas para simular unidades reais
		- <strong style="color: #d79921">Exemplo - Mock</strong>
		  collapsed:: true
			- <p>usa o comportamento da função <strong style="color: #b16286">conectaComBanco()</strong> sem precisar de fato a função. Com isso, são eliminadas as dependências complexas que conectaComBanco() precisa executar.</p> > ```javascript
			  it("mock the conectaComBanco function", function() {
			     mock = sinon.mock(ObjetoDeTeste)
			     expectation = mock.expects('conectaComBanco')
			     expectation.exaclty(1)
			     ObjetoDeTeste.pagamento(100, 1000)
			     mock.verify()
			  }
			  ```
		- <strong style="color: #d79921">Exemplo - Stubs</strong>
		  collapsed:: true
			- <p>Considere a função de pagamento que receve uma função chamada salarioFinal() para fazer um cálculo e retornar um salário.</p> > ```javascript
			  const pagamento = (descontos, salarioBruto) => {
			  //... código omitido
			  salario = salarioFinal(descontos, salarioBruto)
			  return salario
			  }
			  ```
	- <p><strong style="color: #689d6a">Teste de sistema</strong> <span style="color: #3588E9">--></span> analisa e investiga funcionamento completo da aplicação</p>
	  collapsed:: true
		- a integração dos componentes de software com o ambiente operacional são analizados e testados
		- há testes funcionais e não funcioais
		- o teste funcional geralmente é executado por um time independente
		- uso de chapters dentro de squads, caso não se tenha um time dedicado para testes
		- é comum usar um diagrama de casos de uso, como recurso principal de informação
		- também é comum usar historia de usuário no caso de uma abordagem ampla
		- deve ter um fluxo de execução (roteiro)
		- <strong style="color: #d79921">Teste funcional</strong>
			- foca os requisitos funcioansi do sofwatre, sem considerar a sua estrutura interna --> prepcua-se se o comportamento do sitema atendes aos reuisistos funcioanso previamente estabelecidos
			- utiliza algumas tecnicas de modelagem para geração de casos de testes
			- tecnicas de modelagem --> auxiliam na regulação dos casos de testes que iram server para os testes funcioanis
			- chamados por alguns de teste de interface
		- <strong style="color: #d79921">Teste não funcional</strong>
			- busca validar os reuisitoq nao funcionais de um sitema, com por exemplo, o tempo de resposta de uma tela (desempenho)
			- geralmente são assistidos por ferramentas de mercado
			- deve ter uma atençao a questao de acessibilidade --> uso de ferramentas
	- <p><strong style="color: #689d6a">Teste de aceitação</strong> <span style="color: #3588E9">--></span> verifica se o requisito de negocio foi atendido</p>
	  collapsed:: true
		- foco deve ser sempre o requisito de negócio!!
		- recomendado ser um teste assistido --> pode ser feito um teste alfa ou um teste beta
		- não pode ultrapassar um terço do teste funcional do sistema --> regra
	- <p><strong style="color: #689d6a">Teste exploratórios</strong> <span style="color: #3588E9">--></span> ocorre simultaneamente a modelagem (ad-hoc)</p>
	  collapsed:: true
		- baseia nos objetivos de teste, realizado em tempo pré-definido
		- é uma teste mais investigativo
		- é necessário ter um planajamento --> possui um escopo (proposito e prazo)
		- depende da experiencia de quem esta testando
		- o aprendizado ocorre em paralelo
		- a execução do teste é guiada e aprimorada com base na execuação dos teste anteriores
		- os testes não são criados com antecedencia
		- <strong style="font-weight: 600">Vantagens:</strong>
			- Estimula a criativaidade
			- Aumenta a chance de encontrar novos bugs
			- Flexível e adptável
			- Permite uma rápida avaliação
		- <strong style="font-weight: 600">Desvantagens:</strong>
			- Díficil de coordenar
			- Depende das competencias e conhecimentos do testador
		- <p><span style="color: #3588E9">--></span> Um <span style="color: #d65d0e">teste exploratório</span> é optado quando se tem pouca ou nenhuma documentação, quando se tem pouco tempo, quando os teste devem ser melhorados, e quando é necessário fornecer feedback rápido entre sistema e serviço.</p>
		- Pode possuir um roteiro de itens que tem que ser notificados.
		- Tecnicas que podem ser utilizadas: Diagrama de Ishikawa (Diagram de causa e efeito), Five Whays, Teste Oracle, Heurísticas.
	- <p><span style="color: #d65d0e">teste ad-hoc</span> <span style="color: #3588E9">--></span> processo improvizado de busca de falhas.</p>
	- <p><strong style="color: #689d6a">Casos de testes</strong></p>
	  collapsed:: true
		- --> É um teste baseado na especificacao
		- É uma ferramenta que fornece um modo de capturas das entradas de teste, quais as condições que demvem ou não ser atendidas, e os resultados esperados para o sistema.
		- Possibilitam identificar de forma sistematica os aspectos do software que serão testados, e verifica se um dado ou um resultado esperado foi atingido conforme a especificação do sistema.
		- Deve contemplar os casos válidos e os casos inválidos.
		- A especificação deve ser elaborada o mais cedo possivel, visando identificando o maior número de erros antes da construção do sistema.
		- <p>Os casos de testes possuem os seguintes elementos (estrutura):<ul><li>identicação --> identificador do cenário (sigla CN + numero do cenario) masi CT e um sequencial. Exemplo: CN001CT01</li><li>itens de teste --> descreve escopo a que se refere o caso de teste. Exdemplo: validaçao de campos obrigatórios</li><li>pre-condição --> descreve a condição sob as quais o teste deve se ser realizado> Exemplo: nào existe nenhum registo de sinal cadastrado</li></ul></p>
		- <strong style="color: #d79921">Tecnicas:</strong>
			- Partição de equivalenia --> para reduzir o numero de testes ao nivel que seja controlado.
			- Analise do Valor limite --> válida que os valores limites de um determinado dominio e classe equivalencia seja avaliado. Complementa a tecnica de partição de equivalência, e análise as fronteiras do domínio.
			- <p>Gráfico de causa e efeito --> modelo de relacoes logicas entre as causas e efeitos para um comportamente, cada caus espressa um condição pode ser verdadeira ou falsa (booleana).<ul><li>Os casos de testes devem ser projetados para exercitar as regras que definem a relação entra as entradas e saídas desses componenetes.</li><li>É possivel verificar as confiçoes que um sitema esta sendo manipulando de acordo com o previsto, e define quais os casos de testes devem estar modelados para executar um combinação de entras e/ou estimulos descirtos nessa tabela de decisão.</li></ul></p>
	- <p><span style="color: #d65d0e">movile device farm</span> <span style="color: #3588E9">--></span> conceito de um conjunto de dispositivos interligados, que os motivos reais estão ligados a uma ferramenta de automação. Esse conceito permite garantir por exemplo, se um determinado dispositivo vai ficar mais incompatíveis com uma determinada versão.</p>
- ## **Unidade 4 - Desenvolvimentos Orientado à Testes**
  collapsed:: true
	- Débito Técnico --> calcula na evolução da inspecção de código do software os erros que são encontradas, o tempo de correção desses erros e os retestes na ferramenta de inspeção. Se a cada teste o número de erro aumenta, o debito tecnico aumenta.
	- --> quanto maior a cobertura do teste, menor a chance de falha.
	- ferramentas de testes funcionais:
	  collapsed:: true
		- Selenium --> para automatação de testes funcionais. framework que possui um conjunto de ferramentas de código aberto, multi pltaforma, usado para testar aplicacao web pelo brower de forma automatizada. SELECIUM IDE --> recomandedado apra script s de reposiÇão de bug rápidos; WebDriver --> criar suite de testes de automação e regressao masi robusto, recomendados para quando se tem uma coleção associacoes especificas de lingaguagem para utilizar no navegador; Selecium Grid --> processo de teste masi distribuido, é por testar em browser e em ambiente diferentes.
		- --> a ferramenta depdende do contexto da empresa
		- Appium --> framework gratuito para autoamação do steste de swofwtare quen funcions em aplicativos web e mobile. Servirdor HTTP que roda em nodeJS e  ele cria e manipula várias seçoes do websirvsr para diferentes plataformas, como IOS e Android. Pode automatizar teste para desktop.
		- --> a automaçao de testes deve ser feita a partir do momento em que se tem uma versão estável do sistema.
		- Integração continua com automação --> permitir que o desenvolvimento entregue com frequencia software funcional para os usuários.
	- TDD
	  collapsed:: true
		- Desenvolvimento Orientado a Testes - criado por Kent Black
		- modelo que trabalha um ciclo onde devs criam um codigo fonte com teste automatizado que ira falhar.
		- É uma metodologia para desenvolvimento e escrita de código.
	- BDD
	  collapsed:: true
		- Beahviou Driven developr - criado por Dan North
		- o foco esta na regra de negocio, trazendo esta para o código não apenas para o test
		- Dan North criou o primeiro framework BBD para java --> Jbehave; Rbehave para Rub e RSpec
		- É uma prática ageil que permote uma melhor comunicação enre devs, qas area de negocio e pessoas não tecnicas, durante um projeto de softeware, descrevendo um ciclode iteraçoes com saidas bem definidas e resultadno na entrega de software testado e que funciona.
		- sintaxe Gherkin --> acronimo para Given (dado) While (Quando) Then (Então)
		- descoberta - definiçao - formalização - Enteega --> ciclo do BDD
		- <p>A partir dos criterios de aceite, é possivel crair um teste automatizado:</p> > Cenario: visualizar extrato bancário 
		  (Dado que) qeu esteja na tela inicial 
		  (Quando eu) acesso o menu Saldos e Extratos
		  (Então) escolho a opÇão extratos 
		  (E) eu preencho as data de inicio e fim do perido a ser consultato
		  (E) eu seleciono visualizar
		  (Entao) o sitema exibe todas as operações financeiras relacionadas ao perído informado
		- com base nos cenários, tem o teste e a base lógica para o desenolvimento, e essa sintaxe utilizada pelo framework como o cucumber.
		- O BDD necessita de uma boa definição do negócio, para um desenvolvimento mais eficiente.
		- TDD e BDD são metodologias complementares.
	- ATDD
	  collapsed:: true
		- Desenvolvimento orientado a teste de aceitação
		- é realizado de forma colaborativa com levantamento de todos os requisitos e critérios de aceite, para cada estoria além cenários possiveis.
		- Envolve todo o time obrigatoriamente.
		- Funcionmaneto: ocorrem reuniões, os reuisitos são identificados com base na coleta de informações e o problema do cliente.
		- Gherkin é a metologia utilizada.
		- No ATTD se explora todos os cenários possiveis dos critérios de negócio.
		- É possivel com cucumber ou JUnit automatizar o processo de um ATDD.