Is an <strong style="color: #b16286">open-source web based application for CI/CD pipelines</strong>, that is installed on server where the central build takes place, and can be installed on any number of systems. Jenkins is one of the oldest, most popular, and the most complex of all the CI/Cd tools. Written in Java, it <strong style="color: #b16286">describes CI pipeline using "Groovy" language</strong> in a <strong style="color: #d79921">Jenkinsfile</strong>. It aims to automate processes, tied to the build, test, release and deploy stages.

> Note: Jenkins is not ideal for CD, it does not provides visibility into the pipeline process and requires a lot of setup anf maintenance.

<span style="color: #3588E9">--></span> Jenkins can be installed on the local system or in a container, which requires a container runtime and Java isn't required to be installed on the local system.

Job in Jenkins is any runnable task this it controlled by Jenkins

<span style="color:#98971a">Jenkinsfile</span> <span style="color: #3588E9">--></span> text file that contains definitions (instructions). It's possible to have a jenkinsfile for each environment (Dev, Stg, Prod), or one jenkinsfile for a multi stage pipeline.

To backup and restore <span style="color: #3588E9">--></span> <span style="color:#98971a">$JENKIS_HOME</span> folder contains the configuration files and a jobs folder with all the pipelines.
- <span style="color:#98971a">thinBackup</span> <span style="color: #3588E9">--></span> plugin to backup jenkins

<strong style="color: #d79921">Jenkins CLI</strong>

jenkins has a built-in command line interface

the authentication process is throw API Token,

<strong style="color: #d79921">Jenkins Architeture</strong>

Jenkins fllow the master slave architecture --> it has two nodes, a master node and the worker nodes. The master node acts like a controller, which manages the tasks executed on the worker nodes. While Master Node controls the load distribuition on Worker Nodes, the worker node will work as an Execution Node.

User commands can be executed directly on the master node, but it can't be executed on the worker nodes.

Master node is used to schedule the build job and the task, which is done per capacity by the worker nodes, and it's also used to monitor the worker node and record the build result.

Java must be installed on the worker nodes.

Any kind of worker node can be added on a master node.

The master node connects to the worker via Jenkins agent, which is nothing but a jar file.

Jenkins installation is not required on the worker nodes.