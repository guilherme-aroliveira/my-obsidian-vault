## What is Java

Java is a programming language develop by

- <strong style="color: red">Language</strong>
	- Setup
	  collapsed:: true
		- collapsed:: true
		  1. Install JSK on linux
			- <code>$ sudo apt-get openjdk-17</code>
			- <code>$ java --version</code> --> check the Java version
		- collapsed:: true
		  2. Create an Archive
			- <p>jar cf [output_fine_name.jar] [file.class] ... --> generates the output file. Ex: MyApp.jar</p> > When this file is created, it automatically generates a manifest file within the package at path: META-INF/MANIFEST.MF --> this file contains information about the files packaged in the jar file and any other metadata regarding the application.
		- collapsed:: true
		  3. Run the application
			- java -jar MyApp.jar
	- ==Resources==
	  collapsed:: true
		- JVM --> Java Virtual Machine
		  collapsed:: true
			- java computer environment that exist within the system
		- JAR --> stands for Java Archive
		  collapsed:: true
			- it helps compress and cobine multiple Java .class file, dependent libraries and assets into a single distributable package
		- WAR --> stands for Web Archive
		- javadoc --> utility to generate documentation
		  collapsed:: true
			- <p><code>javadoc -d doc MyClass.java</code> --> it's an HTML version of the documentation of the code.</p>
	- ==Conventions==
	- ==Tools==
	  collapsed:: true
		- Maven --> build tool
		  collapsed:: true
			- it uses configuration files where we can specify the steps to be automated, such as the steps in the build process.
		- Gradle --> build tool
		- ANT --> build tool
		  collapsed:: true
			- <p>the build configuration file, is in an XML format. Each section of this file has a target action specified to perform a task</p>```xml
			  <?xml version="1.0"?>
			  <project name="Ant" default="main" basedir=".">
			    <target name="compile">
			      <javac srcdir="/app/src" destdir="/app/build"> </javac>
			    </target>
			  ```
			- <p>The build is run using <code>ant</code> command line utility --> result in running all the specified actions.</p>
			- To run an spcific section --> ant compile [target_action_name]. Ex: ant compile jar
	- ==Libraries==
	- ==Syntax==
	- ==Data Types & Structs==
	- ==Flow Control==
	- ==Functions==
	- ==Object Oriented Programming==
	- ==File Handling==
	- ==Error Handling==
	  collapsed:: true
		- logging implementation
			- ```java
			  import java.util.logging.*; // logging package
			  Logger logger = Logger.getLogger("My Application"); // logger object
			  logger.info("Hello World"); // use loggger object
			  
			  // adds a console handler that outputs all log messages to the console
			  ConsoleHandler handler = new Console.Handler();
			  logger.addHandler(handler);
			  ```
			- java.util.logging --> built in logging framework
				- can be used to log messages to different destinations
			- You can also configure the logger by setting its level and adding handlers for different destinations
	- ==Unit Testing==
	- ==Tips==
---
- <strong style="color: red">Workflow</strong>
	- Build Process
		- Develop ---> Compile ---> Package ---> Document
	- Lorem ipsum
		- lorem ipsum