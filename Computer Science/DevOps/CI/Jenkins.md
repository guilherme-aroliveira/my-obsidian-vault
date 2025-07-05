Is an <strong style="color: #b16286">open-source web based application for CI/CD pipelines</strong>, that is installed on server where the central build takes place, and can be installed on any number of systems. 

Jenkins is one of the oldest, most popular, and the most complex of all the CI/Cd tools. Written in Java, it <strong style="color: #b16286">describes CI pipeline using "Groovy" language</strong> in a <strong style="color: #d79921">Jenkinsfile</strong>. It aims to automate processes, tied to the build, test, release and deploy stages.

>[!note]
>Jenkins is not ideal for CD, it does not provides visibility into the pipeline process and requires a lot of setup and maintenance.

Jenkins can be installed in two ways: 
1. As an application on the local system (Java is required)
2. As a Docker container (Java is not required)

Jenkins uses a Plugin Model to add or remove functionality, any feature that are available for Jenkins is provided as a plugin to be installed. So plugins are a way to connect with Jenkins to other systems (services). 

>[!note]
>Obs: Jenkins is a platform that must be managed, because there is a system underneath. There are updates and patches that needs to be done.

Plugins on Jenkins can also be installed manually by just downloading the plugins at the Jenkins Plugin Portal and saving them in: `/var/lib/jenkins/plugins/`.

When creating Jobs on Jenkins is a good practice to keep spaces out of the job names. Job names with spaces makes things more difficult when working with the job in other ways, like from the command line or from an API.

<strong>Job Types:</strong>
- Free Style --> 


`$JENKIN_HOME` --> primary place that has configuration files
XML is the configutaton of Jenkins --. how it is setup inside the environment
`jobs folder` --> all of the pipelines must backed up
way to backup: filesystem snapshots (not recommend for a long term solution, plugins for backup, shell scripts that backup the Jenkins instance
pluings --> set up the backup directory and define the access permissions

Job in Jenkins is any runnable task this it controlled by Jenkins

<span style="color:#98971a">Jenkinsfile</span> <span style="color: #3588E9">--></span> text file with Piepline DSL Syntax, that contains definitions (instructions). It's possible to have a jenkinsfile for each environment (Dev, Stg, Prod), or one jenkinsfile for a multi stage pipeline. It tells a pipeline what is hould be doing and what services and plugins it should be interacting with.
It defines stages in CI/CD pipeline
similar to groovy
two syntax:
scripted
declarative

To backup and restore <span style="color: #3588E9">--></span> <span style="color:#98971a">$JENKIS_HOME</span> folder contains the configuration files and a jobs folder with all the pipelines.
- <span style="color:#98971a">thinBackup</span> <span style="color: #3588E9">--></span> plugin to backup jenkins

<strong style="color: #d79921">Jenkins CLI</strong>

wget hhtp jenkins-cli.jar --> download the `.jat file`
jenkins has a built-in command line interface, the connect is using curl
the authentication process is throw API Token --> create an APi Token on configure 
`java -jar jenkins-clir.jar https://localhost:8080/ -auth guilherme:TOKEN` --> authentication 
specify the jenkins `.jar` file, specify the server URL, specify the auth and the command itself

example

`java -jar jenkins-clir.jar https://localhost:8080/ -auth guilherme:TOKEN -webSocket -list-jobs`




<strong style="color: #d79921">Jenkins Architeture</strong>

Jenkins fllow the master slave architecture --> it has two nodes, a master node and the worker nodes. The master node acts like a controller, which manages the tasks executed on the worker nodes. While Master Node controls the load distribuition on Worker Nodes, the worker node will work as an Execution Node.

User commands can be executed directly on the master node, but it can't be executed on the worker nodes.

Master node is used to schedule the build job and the task, which is done per capacity by the worker nodes, and it's also used to monitor the worker node and record the build result.

Java must be installed on the worker nodes.

Any kind of worker node can be added on a master node.

The master node connects to the worker via Jenkins agent, which is nothing but a jar file.

Jenkins installation is not required on the worker nodes.

pipeline as a code --> automate pipeline setup with Jenkinsfile. 

Pipelie Concepts
PIpeline --> main block of code, everyhong inside is executed by Jenkins. It has things like: 
- agent --> define where the pipeline is going to run. give a name to the agent, the label or just say any, so it can run on any node.  
- tools --> included from the global tool configuration, like Sonar Scanner or Maven or JDK. receives a name and mentioned the tool included in global tool config. 
- environment --> environment variable that can be used in the steps 
- stages --> the steps that will be executed in a Job
Node/Agent --> both settings, it can define where the pipe is going to be executed.
Stage --> where the actions execution happen. It can have multiple stages
Steps --> part of stages, can be commands like git pull. where the actual command is putted, installation steps. The work that's being done in the pipeline. Ex: deploy code to Azure.
multi stages pipelines --> it's one Jenkins file, multiple stages. These stage could be deb, staging and prod. 


```groovy
pipeline {
  environemnt {
    NEXUS_VERSION = "nexus3"
    NEXUS_PROTOCOL = "http"
    ARTVERSION = "${env.BUILD_ID}" 
  }
}
```


```groovy
pipeline {
  agent any {
    label "master"
  }
  tools {
    maven "Maven"
  }
  stages {
    stage("Build) {
      steps {
        echo "Building..."
      }
    }
    stage("Test") {
      steps {
        // 
      }
    }
    stage("Deploy") {
      // 
    }
  }
}
```

stage 

```groovy
pipeline {
  stages {
    stage("Clone code from VCS") {
        
    }
    
    stage("Maven Build") {
    
    }
    
    stage("Publish to Nexus Repository Manager") {
    
    }
  }
}
```

steps
```groovy
pipeline {
  stage('BuildAndTest') {
    stesp {
      sh 'mvn install'
    }
    post {
      sucess {
        echo 'Now Archiving..'
        archiveArtifacts artifacts: '**/target/*.war'
      }
    }
  }
}
```

