## **Unidade 1 - Banco de Dado Relacionais e Não Relacionais**
collapsed:: true
	- A grande diferença na atulidade é que os recusos tecnologicos permitem que as organizações consigam armazenar um grande volume de dados e trata-los, o poder de processamento e armazenamento permite isso.
	- Dados --> fato do mundo real que pode ser registrado e que tenha uma significado implicíto.
	- Bando de Dados --> coleçao de dados relacionados. Projetado, construído e povoado com dados para um propósito específico.
	- A correta e adequada manipulação dos dados chega-se ate a informação.
	- Um banco de dados é uma representação de uma aspecto do mundo real (mini-mundo ou Universo de Discurso).
	- SGBD --> conjunto de softwares utilizados para criaÇão e manipulaçao de banco de dados
	- Ferramentas CASE (Computer Aided Software Engineering)
	- Modelo de dados --> coleçõa de conceitos utilizados para descrever a estrutura de um banco de dados
	  collapsed:: true
		- M = (E, R, O) --> Estruturas (de dados), Restrições (impostas sobre os dados), Operações (manipulação dos dados)
		- podem ser categorizados de acordo com o nível de abstração:
			- conceitual (ou de alto nível): representação dos dados como ele são; descreve os dados como eles são percebidos no mundo real; modelo de dados de objetos. Exemplo: ER, OO
			- lógico (de implementação): intermediário entre níveis conceitual e físico; modelos de dados de registros. Exemplos: relacional, de redes e hirárquicos. País(Numero(nn),Nome)
			- físico (ou de baixo nível):
				- descreve os dados no nível físico de armazenamento
				- formato e ordenação de registros, índices
	- <p><strong style="color:#689d6a">Banco de Dados Relacionais</strong></p>
	  collapsed:: true
		- Proprosto por Edgar F.Codd, em 1970.
		- No modelo relacional o banco de dados é um conjunto de relações (teoria de conjuntos)
		- Informalmente, uma relação é uma tabela
		- linguagem SQL
		- linhas --> tuplas: lista ordenada de n valores (quantidade de atributos na tabela)
		- colunas --> atributos: nome do papel desempenhado por cado valor "v" em uma tupla
		- relação: conjunto de tuplas r={t1, t2, ... tm}, cada uma das tuplas que constituem uma tabela vão consituir uma instancia da tabela (conteúdo).
		- Todas as tuplas de uma relação têm o mesmo número de atributos, que é o grau de relação. Todas as linhas de uma tabela tem que armazenar a msma quantidade de valores, ainda que sejam valores nulos.
		- tipo --> domínio: conjuntos de valores associados a cada atributo de uma tupla (tipo de valores de um atributo). Exemplo: tipo inteiro, booleano, decimal.
		- restrição de dominio --> o valor de cada atributo em um linha deve ser do mesmo tipo.
		- chave primária --> restrição de chaves: duas linhas diferentes de uma tabela, tem que possuir valores diferentes na chave. Exemplo: CPF de duas pessoas.
		- restrição de integridade entidade: a chave primária não pode assumir o valor nulo.
		- chave estrangeira --> restrição de integridade referencial: permiti definir o relacioamento entre duas tabelas; usadas para manter a consistem entre tabelas. Se um atributo de uam tabela faz uma referencia a um atributo de uma outra tabela, tem que referenciar um valor que existe ou um valor nulo.
		- As operações utilizadas para atualização dos dados em uma relação (tabela) são implementadas pela linguagem SQL.
			- inserção: insere uma nova linha em uma tabela. Pode violar todas as retrições de integridade do modelo relacional.
			- modificação: modifica o valor de um ou mais atributos em nenhuma, uma ou mais linhas de uma tabela. Pode violar todas as retrições de integridade do modelo relacional
			- remoção: remove nenujma, uma ou mais linha de uma tabela. Pode violar apenas a restrição de integridade referencial.
	- <p><strong style="color:#689d6a">Linguagem SQL</strong></p>
	  collapsed:: true
		- SQL --> Structured Query Languge
		- A linguagem SQL possui tres grupso de comands.
		- SQL = DDL + DML + DCL
		- DDL: Data Definition Language --> comandos que atuam na estrutura dos dados, defini a forma como o banco vai ser.
		  collapsed:: true
			- comandos: CREATE, ALTER, DROP
			- ```sql
			  CREATE TABLE Piloto (
			  ...
			  );
			  
			  ALTER TABLE Piloto (
			  ...
			  );
			  
			  DROP TABLE Piloto (
			  ...
			  );
			  ```
			- É mais comum a alteração do conteúdos dos dados do que na estrutura do banco.
		- DML: Data Manipulation Language --> comandos que permitem manipular o conteúdos dos dados
		  collapsed:: true
			- INSERT, DELETE, UPDATE, SELECT
			- INSERT, DELETE, UPDATE --> implementam a tres operações de atualizaçao do modelo relacional
			- ```sql
			  INSERT INTO Empregado VALUES ('888','Pedro','M',5500.00,33,'333')
			  
			  DELETE FROM Empregado
			  WHERE Depto = 44;
			  
			  UPDATE Empregado
			  SET Salario = Salario * 1.2
			  WHERE Depto = 22
			  
			  SELECT E.Nome
			  FROM Empregado E JOIN Departamento D ON E.Depto = D.Cod
			  WHERE D.Nome = 'Financeiro'
			  
			  ### 
			  Consulta aninhada/subconsulta
			  ###
			  
			  SELECT E.Nome
			  FROm EMpregado E
			  WHERE E.CPF NOT IN (SELECT Supervior
			                     FROM Empregado);
			  ```
			- O comando SELECT possui clausulas. FROM --> clausula obrigadtori para consulta
			- JOIN --> operador para fazer cruzamento de duas tabelas
			- COUNT(*) --> conta as colunas
			- GROUP BY --> agrupa os dados
			- ORDER BY --> ordena os dados
		- DCL: Data Control Language --> estabelece o controle de acesso dos usuários
		  collapsed:: true
			- GRANT
			- REVOKE
	- <p><strong style="color:#689d6a">Linguagem NoSQL</strong></p>
	  collapsed:: true
		- NoSQL --> Not only SQL
		- Limitações do modelo relacional --> nem todas as aplicações possuem dados altamente estruturados como no modelo relacional; as ferramentas relacionais (SGBD) impoem controles que nem todas as aplicações precisam.
		- foco em dados semiestruturados e nao estruturads
		- alto desempenho e disponibilidades
		- SGBD's para NoSQL
		  collapsed:: true
			- modelo chave-valor: funciona de forma similar a uma tabela hash
				- foco no alto desempenho, disponibilidade e escalabilidade
				- armazena dados estruturados, semiestruturados e não estruturados
				- contitui-se de uma chave (identificador) associada a um valor (dado)
				- mmecanismo utilizado para rápida recuperação dos dados (eficiencia)
				- reponsabilidade da aplicação interpretar a estrutura dos dados
			- modelo orientado a documentos:
				- comparação com o modelo relacional: coleção esta para tabela assim como documento esta para linha.
				- armazenamento de colecoes de documentos
				- um documento é um objeto complexo em formatos como XML ou JSON
				- estrutura dos dados autodescritiva
				- documentos podem ter elementos de dados diferentes (flexibilidade)
				- Exemplo mondoDB:
					- <code>db.createCollection("projeto",{ capped: true, size: 1310720, max: 500})</code>
					- <code>db.projeto.insert({_id:"P1", Nome_projeto: "ProdutoX", Local_projeto: "São Paulo"})</code>
			- modelo orientado a grafos:
				- permiti armazenar dados na forma de um grafo (Exemplo: rede social)
				- coleções de vertices (nós) e arestas (relacionamento)
			- modelo familia de colunas:
				- particiona uma tebela por colunas (particionamento vertical)
				- cada familia de colunas é armazenada separadamente
		- Algumas ferramentas:
			- Google BitgTable, HBase --> modelo de colunas
			- Amazon DynamoDB e REdis--> chave-valor
			- Apache Cassandra, OrientDB --> hibrido chave-valor e modelo de colunas
			- Neo4J e GraphBase --> modelos de grafos
			- MongoDB e CouchDB --> modelo de documentos
- ## **Unidade 2 - Data Warehouses e Data Lakes**
  collapsed:: true
	- <p><span style="color: #d65d0e">Data Warehouse</span> são repositórios de dados que armazenam a história da empresa, é um <strong style="color: #b16286">banco de dados que armazena dados históricos</strong>, disponivel e acessível para consultas e análises. Uma das características do Data Warehouse é a não-volatilidade, os dados armazenados não podem ser alterados pelos usuários <span style="color: #3588E9">--></span> esses dados descrevem o passado da empresa.</p>
	- <strong style="color: #d79921">Características - Data Warehouse:</strong>
		- <p><strong style="color: #98971a">Integração</strong>: quando um Data Warehouse é projetado, acontece a partir de outras fontes de dados que já existiam antes dele. O conteúdo armzenado, é proveniente da integração de outras fontes de dados que já existiam. Os dados são extraídos das fontes originais, são transformados e depois são carregados/armazenados no Data Warehouse <span style="color: #3588E9">--></span> <strong style="color: #b16286">ETL</strong> (Extração, Trasformação, ETL.)</p>
		- <p>Siglas: OLAP --> processamento analitico online, são dados para analises; SAD --> sistemas de apoio a decisão; EIS --> sistema de informação Executivos;</p>
		- <p>--> Mineração de dados (Data Maning): os dados armazenados também podem ser fontes de dados para um processo de Mineração de Dados.</p>
- ## **Unidade 3 - Ecossistema de Big Data**
- ## **Unidade 4 - Integração de Dados**