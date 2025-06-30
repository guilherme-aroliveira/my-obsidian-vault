jar cf [output_fine_name.jar] [file.class] ... --> generates the output file. Ex: MyApp.jar

When this file is created, it automatically generates a manifest file within the package at path: META-INF/MANIFEST.MF --> this file contains information about the files packaged in the jar file and any other metadata regarding the application.

<code>javadoc -d doc MyClass.java</code> --> it's an HTML version of the documentation of the code.

the build configuration file, is in an XML format. Each section of this file has a target action specified to perform a task

<?xml version="1.0"?>
<project name="Ant" default="main" basedir=".">
<target name="compile">
	<javac srcdir="/app/src" destdir="/app/build"> </javac>
</target>

The build is run using <code>ant</code> command line utility --> result in running all the specified actions.
 
 To run an spcific section --> ant compile [target_action_name]. Ex: ant compile jar

==Error Handling==
logging implementation

import java.util.logging.*; // logging package
Logger logger = Logger.getLogger("My Application"); // logger object
 logger.info("Hello World"); // use loggger object
			  
// adds a console handler that outputs all log messages to the console
ConsoleHandler handler = new Console.Handler();
logger.addHandler(handler);

java.util.logging --> built in logging framework can be used to log messages to different destinations

You can also configure the logger by setting its level and adding handlers for different destinations

# Estrutura de Dados

## Queue

- Tipo de coleção para manter uma lista de priprdade, onde a ordem dos seus elementos, definida pela implementação, determina essa pripridade. Podem-se se criar filas ou pilhas

## Map
Implementacões: HashTable
LinkedHashMap
HashMap

Interface: SortedMap --> implementação: TreeMap

- Cada elemento tem na verdade dois objetos: uma chave e um valor. Valores podem ser deplicado, mas chaves não.

- **SortedMap** que é uma interface de Map, e que permite classificação ascendente das chaves,

- **SortedSet** que estende Set, possiblita a orden,ão natural dos elementos, tal como a ordem alfabetica.

- Uma aplicação dessa interface é a classe **Properties**, que é usada para persistir propriedades/configuracoes de um sistema

# Notação Big O

- O **backend** de uma aplicação é onde estão as regras de negocio, as integrações com outros sistemas.

- **Complexidade assintótica(BigO)** é essencial para saber se estamos escevendo um bom algoritmo ou não. Complexidade assintótica é dividida em duas: a complexidade de tempo e a complexidade de espaço

- **complexidade de tempo** --> estimativa do tempo em que irei levar para executar o meu algoritmo, em essencia o tempo de execução médio do algortimo vai ser o mesmo.

- A **Complexidade assintótica** é um jeito padronizado de conseguir medir o tempo médio de execução do algortimo,independente da máquina em que ele esta rodando.

- Essa **notação de BigO**, é uma notação matemática onde o "O" defini a complexidade de acordo com a entrda N que vier ali. quanto maior o valor de entrada(N), maior é a complexidade do algoritmo.

- **complexidade de espaço** --> uma estimativa do uso de memoria, utilizando a mesma notação de BigO. Sempre usar a menor quantidade de memória possivel dentro do programa, não disperdiçar recurso computacional.

Notação: O(f(n)) --> o de uma função de n
n é o tamanho da entrada e
f é uma função do tamanho da entrada


# Programação Orientada a Objetos

## Modificadores de acesso

- protected -- permite o acesso por outra classe do mesmo pacote, e por uma subclasse, independente do pacote. Only accesible from wthin the same package and from subclasses(child classes) outside the package

- É possivel ter metodos protected
```java
public class MyClass {
		protected void printMessage(String message) {
    		System.out.println(message)
    }
}
```

## Herança

- Toda classe em Java é uma subclasse da classe **Object**

- Métodos  que a classe object possui:
	- getClass --> retorna o tipo do objeto
 	-	equals --> compara se o objeto é igual ao outro
	- hasCode --> retorna um código hash do objeto
	- toString --> converte o objeto para string

```java
public String toString() {
    return name
        + ", $ "
        + String.format("%2.f", price)
        + ", "
        + quantity
        + " units, Total: $ "
        + totalValueInStock();

} /* sobrepõe a operação toString padrão que vem do object */
```

```java
public static void main(String[] args) {
    System.out.println(product.toString())

		/* a chamada do metodo toString não é necessária. O java automaticamente detecta que o objeto esta dentro de um contexto println que espera uma string. */
}
```

- static --> used to indicate that a member belongs to the class itself, rather than to any instance of the class
- herança --> relação "é um"
- super(--> argumentos) --> chama o construtor da super classe
- superclasse(classe base) / subclasse (classe derivada)