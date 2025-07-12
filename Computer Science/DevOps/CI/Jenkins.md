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

>[!example] Example - Token authentication
>```shell
>java -jar jenkins-cli.jar -s http://localhost:8080/ -auth admin:TOKEN -webSocket list-jobs
>```
>To show a help page:
>```shell
>java -jar jenkins-cli.jar -s http://localhost:8080/ help
>```

Instead of using the API Token is also possible to authenticate and using the CLI with the SSH protocol by creating a user and ssh public key.

>[!example] Example - SSH authentication
>```shell
>ssh -i /home/mike/.ssh/jenkins_key -l mike -p 8022 jenkins-server help
>```
>`-l` is the login user which in our example is `mike`
>`-p` is the port which we found out in the previous step to be `8022`
>`-i` flag is used to point to mike private SSH key.

To use ssh to authenticate to jenkins, the public key must be added to the jenkins interface configuration.
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
##### <span style="color: #689d6a">Security</span>

When a Jenkins server is first launched, it's locked by default, and it needs the initial admin password to log in (out-of-the-box security). This is useful to prevent anyone from just coming across a newly installed Jenkins and taking control of it.

Jenkins also allows to create user accounts for individuals with usernames and passwords.

Jenkins can be configured to use different security realms. It provides an interface to manage identities and their authorization to use a resource. The default realm is a user database (built-in).

>[!info]
>A security realm controls how a person is authenticated to access a resource.

Jenkins can delegate authorization to other realms including Lightweight Directory Access Protocol services, also known as LDAP, or systems that use Unix-style users and groups.

All authenticated users are admin by default --> users can do anything. A best practice is to limit admin permission to select users.

Matrix-Based Security can be configured by installing the Matrix Authorization Strategy plugin. With matrix strategy, permission are assigned to each user individually, and these permissions are assigned per action. 

The permissions given to a user in a matrix will apply to all jobs.

>[!note]
>When setting up matrix-based security, assign admin permissions to key accounts. Also assign admin permission to the admin user as well. Failing to assign permissions correctly may lock out admin users.

The "overall" permissions, allows users to at least interact with the Jenkins interface. Without this permission, users won't be able to do anything, even if they got logged in.

Project-based authorization can be used to limit permissions to specific jobs and folders --> the configuration is done the same way as configuring matrix-based authorization.

Jenkins can store and manage sensitive information, which are referred to as a credential (secret). 

Types of credentials:
- Username and passwords
- SSH keys
- Files
- Text strings --> particularly useful for values like API keys or security tokens.

Most commons ways to access credentials in a pipeline:
- `credentials()` function --> used to assign sensitive values to one or more environment variables.
- `withCredentials(){}` build step --> retrieves a secret value and assigns it to a variable. Any step inside it will have access to the secret. Can only be used with credentials that are stored as secret strings.

>[!example] Example - credentials function
>```groovy
>environment {
>  STRING = credentials('secret-value')  
>}
>```
>For most credential types, the function will return one value containing the sensitive information.

When the `credentials` function is used with a username and password type credentials, three variables are returned. The variables specified in the function call will contain both the username and password separated by a colon.

>[!example] Example - credentials function
>```groovy
>environment {
>  LOGIN = credentials('login')  
>}
>```
>`env.LOGIN` --> username:password
>`env.LOGIN_USR` --> username
>`env.LOGIN_PSW` --> password

This method keeps pipeline developers from having to create their own functions for parsing username and passwords over and over again.

>[!example] Example - withCredentials step
>```groovy
>steps {
>  withCredentials([string(credentialsID:'apikey', variable:'APIKEY')]) {
>    sh "./build_script.sh ${env.APIKEY}"
>  }
>}
>```
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

Jenkins supports two pipeline formats: 
- scripted  --> start with the word `node`
- declarative --> start with the word `pipeline`

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

Pipeline Concepts:
- agent --> specifies where a command in a pipeline will be run
- tools --> included from the global tool configuration, like Maven for example. It receives a name and mentions the tool included in global tool configuration.
- environment --> environment variable that can be used in the steps 
- stages --> the steps that will be executed in a Job
- stage --> where the actions execution happen. It can have multiple stages
- steps --> lists the commands that execute something, it can have multiple commands.

Parameters to specify in an agent:
- any --> run on the first available executer (system)
- label --> run on a system with the label parameter: `{ label 'linux' }`
- docker --> run the pipeline inside a docker container using the specified image, either on the jenkins server or another server where docker is running. Useful for projects that need to build enviroximas that are fresh and consistently provisioned on each build.
- none --> at the top of a pipeline is applied to all commands, it allows to defer agent selection to stages. 

>[!example] Example - docker agent
>```groovy
>agent docker {
>  docker {
>    image 'maven'
>  }
>}
>```

Some common pipeline steps:
- echo --> print message
- git --> checkout code from a git repo
- sh --> run a shell script or local command
- archiveArtifacts --> store artifacts created by job

Pipeline Syntax Generator --> used to create snippets of code that can be copied into a pipeline.

An object in Jenkins that needs to be saved, is refereed as an artifact. Artifacts can be compiled binaries like docker image or zip files, it can even be a report (text file) or some sort of document.

The core function `archiveArtifacts` provides a build step for identifying the files to be saved during or after a build. It's often place in the `post` section of a pipeline.

>[!example] Example - artifact
>```groovy
>post {
>  always {
>    archiveArtifacts allowEmptyArchive: true,
> 	   artifact: 'report.txt',
> 	   fingerprint: true
> 	   followSymlinks: false,
> 	   onlyIfSuccessful: true
>  }
>}
>```

The `post` block runs after all sections of a pipeline, so any steps inside the block are run after other operations have finished.

The `Copy Artifact` plugin provides a build step for pulling artifacts from one job into another. The job that creates the artifact must include an option that gives another job explicit permission to copy the artifact.

>[!example] Example - Copy Artifact
>```groovy
>copyArtifacts projectName: 'create-artifact',
>  filter: 'report.txt',
>  fingerprintArtifacts: true,
>  selector: lastSuccessful()
>  
>  options {
>    copyArtifactPermission: 'read-artifact'
>  }
>```
>The fingerprint is used to determine what jobs either created or accesed a file.

When an artifact is created or used, Jenkins generates an MD5 checksum using the file artifact. The checksum and the job where it was created are tracked in an internal database --> becomes the file's fingerprint.

Test Report Formats
- JUnit --> XML documents that describe results of a test. It was originally developed for Java rest reports, but it has become a standard format for test report.
	- JUnit plugin --> gives Jenkins capabilities to collect test reports, publish report as graphs and track trends in test results. 
- Code coverage --> technique that tracks the line of code that are accessed during a test.
	- Code Coverage API Plugin --> collects and publish coverage reports
	- JaCoCo and Cobertura--> report formats very popular for testing Java applications, but due to its popularity it has been used by other languages and tools.
###### <span style="color: #98971a">Pipelines Variables</span> 

Jenkins exposes three different types of variables that can be used: Environment variables,  Current build variables and Parameters.

Environment variables --> named with all capital letters, can be scoped globally for an entire pipeline or locally in a stage.

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

Environment Variables can be reference in different ways in a pipeline depending on how they are being used. The best practice is to stay consistent throughout a pipeline script.

>[!example] Environment variables - referencing
>proceeded by the keyword "env"
>```groovy
>echo env.MAX_SIZE 
>echo "${env.MAX_SIZE}" // if being used in a string
>```
>referenced by their name
>```groovy
>echo MAX_SIZE
>echo "${MAX_SIZE}" // if being used in a string
>```
>Obs: the use of `{}` to wrap a variable name in a string is optional

currentBuild Variables --> allow pipeline steps to reference the state of a build while it's running. Can be useful for dynamic operations that need to do something specific based on a previous step or a certain status in the build. 

All the the current build variables area actually properties of one variable named `currentBuild`, which is case sensitive. The properties are also case sensitive and use the CamelCase format.

>[!example] Example - currentBuild Variables
>```groovy
>currentBuild.startTimeInMillis
>currentBuild.Duration
>currentBuild.currentResult
>```
>The currentBuild variables also needs to be proceeded by a `$` if they are used in strings.

Parameter Variables --> another type of variables that get their values at the time the job is triggered. Parameters are defined in the `parameters` block.

Each parameter definition must include a name, a default value, and a description that explains the type of value that should be entered. Parameters names are assigned using all capital letters.

>[!example] Example - Parameter Variables
>```groovy
>pipeline {
>  agent any
>  parameters {
>    ...
>  }
>}
>```
>To call a parameter:
>```groovy
>params.PARAMETER_NAME
>```

Parameters Types that can be used on pipelines: 
- String --> best used fro single word values
- Text --> useful if needs to pass a long block of text that contains multiple lines.

>[!example] Example - String
>```groovy
>string(name: 'FATHER', 
>  defaultValue: 'Vader',
>  description: 'Enter your fathers's name.')
>```

- Boolean --> let it pass in true or false values. Represented by a check mark in the Jenkins interface. 

>[!example] Example - Boolean
>```groovy
>booleanParam(name: 'RUN_TESTS',
>  defaultValue: false,
>  description: 'Toogle this value to run tests.')
>```

- Choice --> present the user with a list of options to choose from. When is it created, the options are entered as a list.

>[!example] Example - Choice
>```groovy
>choice(name: 'AWS_REGION'
>  choices: ['us-east-1'],
>    'us-east-2',
>    'us-east-1',
>    'us-west-2',
>  description: 'Select a region for deployment.')
>```

- Password --> can be used to enter sensitive values like passwords and API keys. Password values are entered in the same way that string parameters are entered.

>[!example] Example - Password
>```groovy
>password(name: 'DATABASE_PASSWORD',
>  defaultValue: 'DATABASE_PASSWORD',
>  description: 'Enter the database password')
>```

Obs: When defining a pipeline with parameters, Jenkins only applies the parameters after the first run, which may encounter erros, if default values are not available.
###### <span style="color: #98971a">Conditional Expressions</span> 

To set up a pipeline condition just use the `when` keyword inside a stage block. The `when` block uses three build conditions to determine if the steps in a stage should be run: branch, environment and expression.

>[!example] Example - condition
>```groovy
>pipeline {
>  agent any {
>    stages {
>      stage ('XYZ') {
>        when {}
>      }
>    }
>  }
>}
>```

Branch conditions are useful when the pipeline is interacting with a version control system like GitHub. This allows to only run stages for a specific branches in a repo.

Environment conditions evaluate to true, if the specified environment variable is present and it contains the specified value.

>[!example] branch and environment condition
>```groovy
>when { branch 'default' }
>
>when {
>  environment name: 'DEPLOY_TO', 
>  value: 'production'
>}
>```

Expression conditions provide the most flexibility for conditions statements. Groovy expressions can be used along with parameters and other variables to build a statement that runs true or false.

Groovy operators: https://groovy-lang.org/operators.html

>[!example] expression condition
>```groovy
>when {
>  expression {params.ENVIRONMENT == 'PRODUCTION' }
>}
>```

Input step can be used to control the flow of a pipeline. The input step pauses a triggered pipeline and waits for manual interaction.

>[!example] Example - input step
>```groovy
>steps {
>  input message: 'Cnnfirm deployment to production', ok: 'Deploy'
>  echo "Deploying to ${params.ENVIRONMENT}"
>}
>```
###### <span style="color: #98971a">Jenkinsfile</span> 

To increase automation and track changes to pipelines the option to get pipelines from source control management can be used.

A jenkinsfile format can be used to capture the pipeline definition as code. This definition is a text based file with DSL Syntax. It can track changes made to the pipeline dentition, and it also lets define the entire project configuration itself.

A jenkinsfile file can be used to captura definition for tools, option for the project, and triggers to run a project, and more.

Storing the jenkinsfile in a repo also allows development teams to use a GitOps approach --> the repository becomes the single source of truth. 

Jenkins can interact with many different types of version control systems, like Mercurial or Subversion, but the Git system it the most popular.

To use the jenkinsfile:
- create a pipeline job
- select the option GitHub project --> creates link to the repo on the Jenkins interface, it allows to go branch and forth between Jenkins and GitHub
- select the option "GitHub hook trigger" --> enables the trigger that will allows Jenkins to respond to a webhook from GitHub
- select "Pipeline script from SCM" option in Pipeline section

>[!note]
>Obs: The project must run at least on successful build before it connects to GitHub. This allows Jenkins to read the configuration from the repository.

It's also necessary to create the webhook in GitHub so that the job gets triggered on each push to the repo. It needs the URL for the Jenkins server with the additional information: `/github-webhook/` --> this is key to have integration.

With jenkinsfile any supporting files and scripts can be stored to build a project. This can enable a pipeline to run build commands and scripts that might be far too complex to run directory in the pipeline.

Combining multiple steps into a single script also keeps the pipeline definition clear and easy to debug. 

Jenkins uses two build steps to run external commands:
- `sh(...)` --> runs shell commands on Linx, macOS
- `bat(...)` runs shell commands on Windows
- `dir(...)` --> takes path as an argument. 

>[!example] Example - scripts
>```groovy
>dir("${env.WORKSPACE}/environments/test")
>sh(''''
>  terraform init
>  terraform plan
>    ''')
>)
>```

Obs: for scripts that are located in a repo, a relative path can be used and must match the format expected by the system running the command. If the script or command is located outside the workspace, where the repo was checkout, an absolute path must be used.

>[!example] Example - script paths
>Relative paths:
>```jenkinsfile
>sh('./scripts/build.sh')
>bat('..\scripts\build.bat')
>```
>Absolute paths:
>```jenkinsfile
>sh('/bin/build.sh')
>bat('C:\bin\build.bat')
>```

Another way to connect Jenkins to a version control system is displaying a status badge --> dynamically generated image that communicate build status. To enable status badges, the plugin Embeddable Build Status must be installed. 

A multi stage pipeline it's jenkinsfile with multiple stages. These stages could be dev, staging and prod for example.

>[!example] Example - Multi Stage Pipeline
>```groovy
>pipeline {
>  agent any
>  stages {
>    stage("Dev") {
>      steps {
>        // Get some code from a GitHub repository
>        git 'https://github.com/user/go-webapp.git'
>      }
>    }
>    stage("UAT") {
>      steps {
>        // Get some code from a GitHub repository
>        git 'https://github.com/user/go-webapp.git'
>      }
>    }
>  }
>}
>```