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
##### <span style="color: #689d6a">Jenkins Architeture</span>

Jenkins follows the **Controller–Agent architecture** designed to scale build and automation workloads across multiple machines.

The Jenkins Server which is also referred to as the Jenkins Controller provides a web interface to manage the overall configuration of the Jenkins Server. 

A best practice is to limit the Jobs that are run on the Controller to free up resources and only run jobs on other servers which are referred as node or agents --> frees up CPU, memory, and hard drive space on the Jenkins controller. 

The Jenkins Controller should use its resources for management tasks like scheduling jobs.

>[!info]
>Node: a server or system connected to a Jenkins Controller over a network. Node provide the Jenkins Controller with a compute resource for running jobs.
>
>Agent: a process running on a node that manages jobs an reports status to the Jenkins controller.

The agent runs the commands in the Job definition and reports the status back to the Jenkins Controller.

Node Types:
- SSH nodes --> jenkins connect to a server as a specific user with an SSH key. Used if the node os not on the same network as the Jenkins Controller.
- Docker nodes --> nodes an agents that run as containers. The Jenkins Controller runs jobs in a newly created container on each build.

Obs: User commands can be executed directly on the Jenkins Controller, but it can't be executed on the agents.

Jenkins uses the directory defined on the Remote root directory option on the Nodes configuration to creates workspaces.

>[!example] Example - Agent configuration
>```groovy
>pipeline {
>  agent {
>    label 'linux'
>  }
>}
>```
>---
>```groovy
>pipeline {
>  agent {
>    docker { image 'public.ecr.aws/docker/library/maven:latest'}
>  }
>}
>```

When using a Docker agent, the server may need additional storage and memory resources. As the server downloads images, it will need space to store them. In this approach the Jenkins Server needs to have the Docker Pipeline plugin installed.

A pipeline may also need to be configured to install any tools that it needs to run. This gives a pipeline more control over the version of a specific tool.

>[!example] Example - Tool configuration
>```groovy
>pipeline {
>  agent { label 'linux' }
>  tools {
>    maven 'Maven-3.8.4'
>  }
>}
>```

When Jenkins uses a pipeline from a repository, the first checkout is on the Jenkins Controller --> allows the Jenkins to read and process the jenkinsfile to get the project configuration.

When a Jenkins starts running the Job on an agent, the code that was initially checkout by the Controller won't be available. In this case the pipeline must be updated to checkout the code so that it can be used on the agent.

>[!example] Example - Checkout code
>```groovy
>steps {
>  sh 'git --version'
>  git branch: 'main',,
> 	 url: 'https://github.com/jenkinsci/jenkins.git',
> 	 credentialsId: 
>}
>```
##### <span style="color: #689d6a">Jenkins CLI</span>

Jenkins has a built-in command line interface, that can be connected via curl. The authentication process is throw an API Token that must be created.

```shell
java -jar jenkins-cli.jar -s http://localhost:8080/ help

java -jar jenkins-cli.jar -s http://localhost:8080/ -auth admin:TOKEN -webSocket list-jobs
```

Instead of using the API Token is also possible to authenticate and using the CLI with the SSH protocol by creating a user and ssh public key.

`curl -Lv http://localhost:8085/login 2>&1 | grep -i 'x-ssh-endpoint'`

`ssh -i /home/mike/.ssh/jenkins_key -l mike -p 8022 jenkins-server help`
1. `-l` is the login user which in our example is `mike`
2. 1. `-p` is the port which we found out in the previous step to be `8022`
3. 1. `-i` flag is used to point to `mike's` private SSH key. Remember, we have already added the public key in the Jenkins configuration.
##### <span style="color: #689d6a">System Admin</span>

primary place to backup To backup and restore <span style="color: #3588E9">--></span> <span style="color:#98971a">$JENKIS_HOME</span> folder contains the configuration files (config.xml --> the configuration of Jenkins) and a jobs folder with all the pipelines. jobs folders --> contains all the pipelines.
- <span style="color:#98971a">thinBackup</span> <span style="color: #3588E9">--></span> plugin to backup jenkins

`$JENKIN_HOME` --> primary place that has configuration files
XML is the configutaton of Jenkins --. how it is setup inside the environment
`jobs folder` --> all of the pipelines must backed up
way to backup: filesystem snapshots (not recommend for a long term solution, plugins for backup, shell scripts that backup the Jenkins instance
pluings --> set up the backup directory and define the access permissions

monitoring jenkins with a prometheus plugin - set up a jenkins server
`/etc/prometheus/prometheus.yml`
add tgis config on promethets yaml file
```yaml
- job_name: 'Jenkins'
  metrics_path: '/prometheus/'
  static_configs:
  -  targets: ['IP:8080']
```
`IP:8080/prometheus` if the plugin is installed, the data comes automatically, for Prometheus to scrape Jenkins.
all the data scraping by Prometheus can be seen on the Prometheus UI search bar 
##### <span style="color: #689d6a">Jobs</span>

When creating Jobs on Jenkins is a good practice to keep spaces out of the job names. Job names with spaces makes things more difficult when working with the job in other ways, like from the command line or from an API.

<strong>Job Types:</strong>
- Freestyle project--> most commonly used, lets freely control the way Jenkins manages the tasks to be automated.
- Pipeline --> useful for project that are more complex than freestyle jobs.
- Multi-configuration project --> useful when it needs to have multiple jobs that o the same thing but for different combinations of parameters.
- Multibranch Pipeline --> suited for working with code repositories, can be used to configura different jobs for different branches belonging to the same repo.

Build triggers
A trigger is any action that starts a job. By default, the job can be started manually.
Trigger build remotely --> lets processes outside of Jenkins start jobs by accessing a URL through the Jenkins web API.
Build after --> lets Jenkins start jobs immediately after some other job are finished. Good for Jobs that depend on each other. 
Build periodically --> useful for jobs that need to be run hourly, daily, weekly, and son on. The field to specify the schedule use the cron format. 
GitHub hook --> good for projects that are tied to GitHub. This option allows Jenkins to start jobs based on activity in GitHub like releases, tags, or other types of commits. 
Poll SCM --> can also start a job based on activity in a repo, but it's not efficient as triggering from GitHub hook.

Build environment
This section gives control over the space where the job will run and some steps to take when the jobs is actually running.

Each time when a Job runs, it uses a specific directory on the Jenkins system called the workspace. This is where the job stores any files that are generated during the build. By default, any files created by a job and saved to the workspace will stay there between job runs.

using parameters: 
Jenkins supports creation of Jibs that accepts different types of parameters, including strings, booleans, and multiple choices. These vaules are then ejected into the job and accessed as environment variables --> must follow the corect format according to the system that will work on.
in windows: `%STRING_PARAMETER%`
in shell: `$STRING_PARAMETER` 
example 
```shell
#! /bin/bash
echo "VERSION_NUMBER = $VERSION_NUMBER"
```

Jenkins uses a format similar to cron for scheduling jobs. Execution times are defined by an expression representing the schedule.
```text
*****
|||||
|||||___
||||____
|||___
||__
|__
```

`*(minute 0-59) *(hour 0-23) *(day of the month 1-31) *(Month 1-12 or Jan-Dec) *(Day of the week 0-6 or Sun-Sat)`
Example `*****` --> 
Jenkins Scheduler aliases
Use H for hashed values to spread out job around the desired time
Use simple aliases for general times. Example: `@hourly, @daily, @midnight, @weekly, @mounth, @annaually`
time zones are relative to the server

creating folders
folders provides a namespace that is separate from other folder in Jenkins. Any jobs and views in a folder re isolated and can even have the same name as item in other folders. 
when a folder is deleted, everything thar is in the fodler will be deleted, including jobs and pipelines
##### <span style="color: #689d6a">Pipelines</span>

Jenkins supports two pipeline formats: scripted and declarative. Scripted pipelines start with the word `node` and Declarative pipelines start with the word `pipeline`
Scripted pipelines use a domain-specific language or SAL based on Groovy, which is a scripting language fir the Java virtual machine. 
Declarative pipelines are an evolution of DSL pipelines --> the syntax was developed to more easily capture the complete configuration os a project as code.

>[!example] Example - declarative format
>```groovy
>pipeline {
>  agent any
>  stages {
>    stage('Hello') {
>      steps {
>        echo 'Hello World'
>      }
>    }
>  }
>}
>```
>In the stages section is required to have at least one stage with at least one steps section. 
>
>The steps section lists the commands that execute something, it can have multiple commands.

The agent section specifies where command in a pipeline will be run.  
Parameters to specify an agent:
- any --> run on the first available executer (system)
- label --> run on a system with the label parameter: `{ label 'linux' }`
- docker --> run the pipeline inside a docker container using the specified image, either on the jenkins server or another server where docker is running. Useful for projects that need to build environemtns that are fresh and consistently provisioned on each build.
- none --> at the top of a pipeline is applied to all commands, it allows to defer agent selection to stages. 

>[!example] Example - docker agent
>```groovy
>agent docker {
>  docker {
>    image 'maven'
>  }
>}
>```

Pipeline steps
echo --> print message
git --> checkout code from a git repo
sh --> ru na shell scrit or locl command
archiveArtifacts --> store artifacts created by job

Pipeline Syntax Generator --> used to create snippets of code that can be copied into a pipeline.

variables
environment --> named with all capital letters, can be scoped globally for an entire pipeline or locally in a stage.

current build --> allow pipeline steps to reference the state of a build while it's running. Can be useful for dynamic operations that need to do something specific based on a previous step or a certain status in the build. All the the current build variables area actually properties of one variable named `currentbuild`. Example: `currentBuild.startTimeInMillis` --> is case sensitive. must be proceeded by a dollar sign `$` if the ere used in strings.


parameters

>[!example] Example - environment variable
>Globally
>```groovy
>pipeline {
>  agent any
>  environment {
>    MAX_SIZE = 10
>    MIN_SIZE = 1
>  }
>}
>```
>Locally
>```groovy
>pipeline {
>  ...
>  stages {
>    stage ('Scale by 10x') {
>      environment {
>        MAX_SIZE = 100
>        MIN_SIZE = 10
>      }
>    }
>  }
>}
>```

environment variables can be reference in different ways in a pipeline depending on how they are being used: The best practice is to stay consistent throughout a pipeline script.

echo env.MAX_SIZE
echo MAX_SIZE
echo "$env.MAX_SIZE" --> using in a string or with `{}`
echo "$MAX_SIZE" --> using in a string or with `{}`


<span style="color:#98971a">Jenkinsfile</span> <span style="color: #3588E9">--></span> is text file with Piepline DSL Syntax, that contains definitions (instructions). It's possible to have a jenkinsfile for each environment (Dev, Stg, Prod), or one jenkinsfile for a multi stage pipeline. It tells a pipeline what is hould be doing and what services and plugins it should be interacting with.
It defines stages in CI/CD pipeline
similar to groovy
two syntax:
scripted
declarative

pipeline as a code --> automate pipeline setup with Jenkinsfile. 

Pipelie Concepts
PIpeline --> main block of code, everyhong inside is executed by Jenkins. It has things like: 
- agent --> define where the pipeline is going to run. give a name to the agent, the label or just say any, so it can run on any node.  
- tools --> included from the global tool configuration, like Sonar Scanner or Maven or JDK. receives a name and mentioned the tool included in global tool config. 
- environment --> environment variable that can be used in the steps 
- stages --> the steps that will be executed in a Job
the node is the build agent
Node/Agent --> both settings, it can define where the pipe is going to be executed.
Stage --> where the actions execution happen. It can have multiple stages
Steps --> part of stages, can be commands like git pull. where the actual command is putted, installation steps. The work that's being done in the pipeline. Ex: deploy code to Azure.
multi stages pipelines --> it's one Jenkins file, multiple stages. These stage could be dev, staging and prod. 


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
    steps {
      sh 'mvn install'
    }
    post {
      success {
        echo 'Now Archiving..'
        archiveArtifacts artifacts: '**/target/*.war'
      }
    }
  }
}
```

multi stage pipeline
```groovy
pipeline {
	agent any{
	
		stages {
			stage("Dev") {
				steps {
					// Get some code from a GitHub repository
					git 'https://github.com/user/go-webapp.git'
				}
			}

			stage("UAT") {
				steps {
					// Get some code from a GitHub repository
					git 'https://github.com/user/go-webapp.git'
				}
			}
		}
	}
}
```

Build agents --> is the system that run the entire workload. The entire CI/CD pipeline runs via the build agents. 