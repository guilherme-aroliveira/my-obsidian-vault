## **Introduction**
---
<span style="color: #d65d0e">DevOps</span> is the <strong style="color: #b16286">practice of development and operations engineers working together</strong> through the entire software development life-cycle, following <span style="color: #d65d0e">Lean</span> and <span style="color: #d65d0e">Agile principles</span> that allows them to deliver in a rapid and continuous ways.

> [!note] 
> DevOps is a <strong style="color: #b16286">cultural change</strong> that requires trust, transparency, communication, coordination and discipline across teams.

<span style="color: #3588E9">--></span> Technology is the enabler of innovation. Technology alone is not going to drive innovation.

DevOps has three dimensions: culture, methods and tools.

Working in <span style="color: #d65d0e">small batches</span> is a <strong style="color: #d79921">concept</strong> from <span style="color: #d65d0e">Lean Manufacturing</span>. It's important in situations when fast feedback is required. Feature size support frequent releases, features should be completed in a script.

<strong style="color: #d79921">Working DevOps</strong> is all about facilitating a cultura of teaming and collaboration, agile development as a shared discipline, automate relentless, push smaller releases faster.

DevOps <strong style="color: #b16286">seeks to breaking big projects down</strong> to deliver a continual series of <strong style="color: #d79921">small changes</strong> that are more manageable DevOps reduces the risk of large projects.

<strong style="color: #d79921">In Devops</strong> <span style="color: #3588E9">--></span> network design is defined by its architecture
* <span style="color: #3588E9">--></span> ephemeral infrastructure created for each new deployment

DevOps <strong style="color: #d79921">behaviors</strong>
* shared ownership and high collaboration
* ephemeral infrastructure as code
* automated self-service
* fast feedback loops that data-driven

<span style="color: #d65d0e">Social Coding</span> <span style="color: #3588E9">--></span> open source for inner source. 
- All repositories are public and everyone is encouraged to contribute.
- The person who owns the repository is still in complete control of the contributions. The repository owners are in full control.
- <strong style="color:#c6554f">Workflow</strong>
	- GitHub issue <span style="color: #3588E9">--></span> Discuss <span style="color: #3588E9">--></span> Fork <span style="color: #3588E9">--></span> Merge
- <strong style="color:#c6554f">Principles</strong>
	- Developers are considered as equal team members, and they can leverage another team's code.
	- Company saves money as code is reused.

> [!info]
> Social coding is something that open source communities have been doing for years. What’s new is bringing these concepts into the enterprise and coding as a community on internal projects.

<span style="color: #d65d0e">Pair Programming</span> is an <strong style="color: #b16286">aspect of social coding</strong> that its taken from <span style="color: #d65d0e">Extreme Programmin (XP)</span>. It consist of two programmers sharing a single workstation. The programmer at the keyboard is usually called driver and the other is called navigator, in every 20 minutes they switch.

<strong style="color: white">Benefits</strong> of <span style="color: #d65d0e">Pair Programming</span>: higher code quality, defects found earlier, lower maintenance costs, skills transfer, board understanding of the code base.

<span style="color: #d65d0e">Git</span> <span style="color: #3588E9">--></span> industry standard for version control.

> [!note ]
> DevOps benefits from Git because it can handle projects of all sizes, enables non-linear collaboration, and tracks version control to ensure code quality

---
##### <span style="color:#689d6a">Organization impact of DevOps</span>

Part of becoming a DevOps organization is to first become <span style="color: #d65d0e">Agile</span>, because <strong style="color: #b16286">Agile is a fundamental tenet of DevOps</strong>. 

> Agile teams must be small, dedicated teams, cross-functional teams, self-organizing teams.

<span style="color: #d65d0e">Conway's law</span> <span style="color: #3588E9">--></span> "Any organization that designs a system will produce a design whose structure is a copy of the organization's communication structure" <span style="color: #3588E9">--></span> The Conway's law implies that a company's design is a direct reflection of the company's communication structure.

It's better to <strong style="color: #b16286">organize teams around business domain</strong>. If we don't do it, we are not going to get the full benefit of DevOps. Each team should have a mission that aligns with a business domain.

Teams have end-to-end responsibility for what they build, and also should have a long-term mission usually around a single business domain.

<span style="color: #3588E9">--></span> If we're not doing development, then we're not doing DevOps we're doing just Ops.

DevOps is a <strong style="color: #d79921">mindset</strong> that the whole organization adopts.

> [!warning] Obs: There's no such thing as a DevOps team. That's an anti-pattern, it causes more problem that it would solve.

<strong style="color: #b16286">Create cross-functional teams</strong> so that everyone is dealing with teammates instead of ticket queues.

Make people responsible by putting developer on pager duty or having them own the service level agreement for the product and services they build.

The DevOps organizational objective should be attain a shared consciousness with distributed local control.

We should measure and reward what we want to improve.

<span style="color: #3588E9">--></span> DevOps changes the objective of problem resolution from failure prevention to <strong style="color: #d79921">failure recovery</strong>.

<strong style="color: #d79921">Actionable metrics</strong> provide meaningful ways to measure the processes and work toward a goal. 

Actionable metrics examples: reduce time to market, increase overall availability, reduce the time to deploy, detect defects before production, more efficient use of infrastructure, quicker performance feedback.

> [!note] 
> Having information when it matters is important for making informed decisions.

---
##### <span style="color:#689d6a">Site Reliability Engineering</span>

<span style="color: #d65d0e">Site Reliability Engineering</span> <span style="color: #3588E9">--></span> "Is what happens when a software engineer is tasked with what is used to be called operations."

<strong style="color: #d79921">Tenets of SRE</strong><ul><li>Hire only software engineers</li><li>Site reability engineers work on reducing toil through automation</li><li>SRE teams are separated from development teams</li><li>Stability is controlled through error budges</li><li>Developers rotate through operations</li></ul>
DevOps maintains stability by using automation through Continuous Delivery pipelines, and by making sure that everyone is responsible for the code that runs in production.

Both seek to make development and operations visible to each other. Both requires a blameless culture. The objective of both is to deploy software faster with stability.

<span style="color: #3588E9">--></span> SRE and DevOps can be use together to both maintain and use computer infrastructure.
##### <span style="color:#689d6a">Security by Design</span>

Involve and collaborate with the security team to understand and experience the smooth deployment if new features.

Developers can develops secure applications with DevOps.

<span style="color: #d65d0e">Secure SDLC</span> <span style="color: #3588E9">--></span> process that involves security testing and its best practices in the existing development model<ul><li>It describes how security fits into the different phases of the software development life-cycle</li><li>Risk assessment <span style="color: #3588E9">---></span> Threat modeling and design review <span style="color: #3588E9">---></span> Static analysis <span style="color: #3588E9">---></span> Security testing and code review <span style="color: #3588E9">---></span> Security assessment and configuration</li></ul>
- <strong style="color: #d79921">Mapping secure SLDC phases</strong>
	- <span style="color: #98971a">Requirements stage:</span>
		- Determine operational standards
		- Define security requirements
		- Include monitoring and metrics
	- <span style="color: #98971a">Design stage:</span>
		- Perform threat modeling to secure the design architecture
		- Secure the deployment pipeline
		- Create unit test to counter common threats
	- <span style="color: #98971a">Develop stage:</span>
		- Perform analysis to check for vulnerabilities in code
		- Include automation and validation
		- Use security tasks and security in the scrum
	- <span style="color: #98971a">Test stage:</span>
		- Incorporate vulnerability scans
		- Strive for failure
		- Paralelize security testing
	- <span style="color: #98971a">Deploy stage:</span>
		- Include automated launch of deployment scripts
		- Use deployment and rollback
		- Perform production security test

<span style="color: #d65d0e">DevSecOps</span> <span style="color: #3588E9">--></span> set of principles that automates security integration across the software development life cycle (SDLC) <ul><li>Discipline of adding security early in the application development life cycle to reduce risks</li><li>DevOps with an emphasis on security</li></ul>
* <strong style="color: white">Benefits</strong>
	* Delivery high-quality software quickly and at an affordable price
		* decreased time spent on fixing security vulnerabilities by reducing the need to repeat a procedure to minimize development cost
		* integrated security results in better code
		* increased delivery rates and reduced expenses
	* Increased security through proactive measures
		* security is checked from the start of the development cycle
		* fewer patches are necessary
	* Vulnerability patching at an accelerated pace
		* manages recently discovered security flaws
	* A modern approach to automation
		* including [[Cyber Security]] testing in an automated test suite
		* checking that all included software dependencies are up to date
		* making sure that software passes security unit testing
		* using static and dynamic analysis to teste and secure code before releases
		* enabling immutable infrastructure
	* The cycle of repetition and the ability to adapt
		* enables repeatable and adaptive process
		* guarantees that security is implemented uniformly throughout the environment
		* speeds up recovery after a security incident
## **Linux**
---
Whenever a Linux system builds up, it starts with just one process with a process ID of one. This is the root process and kicks off all the other processes in the system. By the time the system boots up completely, we have a handful of processes running. This can be seen by running the PS command to list all the running processes.

IDs are unique and two processes cannot have the same process ID.

The text based command line interface that helps you run commands to interact with the operating system is called the Linux shell

there are different kinds of shells such as The Bourne Shell, the C Shell, Z Shell, born again Shell, which is known as Bash. And each of these shells behave differently

Every Linux system has a super user known as the root user. The root user has no restrictions on the system and can perform any task, which is why in most production environments or enterprise environments, access to the root user is restricted and you will almost never log in to the systems as a root user. To edit sudo rules --> /etc/sudoers
##### **<span style="color:#689d6a">Linux Commands</span>**

echo $SHELL --> to see which shell you are on

Basic Commands

commands - direcotires

commands - files

User accounts

Download Files

Check OS Version
##### **<span style="color:#689d6a">VI Editor</span>**
##### **<span style="color:#689d6a">Package Management</span>**

package managers --> help you install various software on the Linux system

CENtOS uses an RPM based package manager just like Red Hat Enterprise Linux or Fedora. RPM stands for Red Hat Package Manager.

A software is packaged into a bundle with the extension .RPM

- To install the package --> rpm -i telnet.rpm
	- -i --> for install
	- telnet.rpm --> package name

to Unistal the packge --> rpm -e telnet

- to query the database --> rpm -q telnet
	- get details about an installed package

RPM requires you to point it to the exact location where the RPM package is available. You then install that package on the system. So simply installing Ansible with the RPM command would not take care of installing Python and other dependent libraries if they are not. already installed

- Yum is a high level package manager that uses RPM underneath.
	- yum install ansbile[package] --> installs Ansible and all of its dependent packages.

Yum searches software repositories that act as warehouses containing hundreds and thousands of RPM package files. Under the hood, yum still makes use of the RPM Package manager. yum searches these repositories, finds the required packages and dependencies, and installs all of them in the right order

The information about the repository in a configuration file at path /etc/yum.repos.d

Every operating system comes bundled with its own set of repositories

So to see the list of repositories available on a system --> yum repolist

- To see a list of installed or available packages --> yum list
	- yum list  { package_name } --> to search for a particular package
	- It provides the package name and version, and if it's an installed package or just an available package.

To remove an installed package --> yum remove [package_name]

to list all available versions of a package --> yum --showduplicates list [package_name]

To install a specific version of a package --> yum install [package_name-version]
- Ex: yum install ansible-2.4.2.0
##### **<span style="color:#689d6a">Service Management</span>**

services in Linux help you configure software to run in the background and make sure that they run all the time automatically when servers are rebooted as well as they follow the right order of startup.

service { service_name } start --> to start a service
- Ex: service httpd start
- The service command uses the system cuddle utility underneath

systemctl start httpd --> newer method to start a service
- stands for system control
- command used to manage services on a system demanaged server

systemctl enable --> configure a service to start automatically when the system boots up

A systemd service is configured using a systemd unit file. These files may be located at <code>/etc/systemd/system</code>. The file must be named with the name that you eventually want the service to be known as.
```bash
	[Unit]
	Description=My python web application
	[Service]
	ExecStart=/usr/bin/python3 /opt/code/my_app.py
	ExecStartPre=/opt/code/configure_db.sh
	ExecStartPost=/opt/code/email_status.sh
	Restart=always #automatically restart in case it crashes
	[Install]
	WantedBy=multi-user.target
```
- ExecStart --> directive to specify the command that you will be using to run your application.
- { Install } --> section to configure the service to run after a particular service that runs at boot up

systemctl daemon-rel --> let system know that there is a new service configured.
##### **<span style="color:#689d6a">Network</span>**

ip link --> to list and modify interfaces on the hos

ip addr --> to see the IP addresses assigned to the network interfaces

ip addr add --> to set IP addresses on the network interfaces --> are only valid until a restart

ping IP_address -->

route --> to view the routing table (to see existing routing configuration on a system)

ip route add --> used to add entries into the routing table

To configure a gateway on system B to reach the systems on network 2.0 --> ip route add 192.168.2.0/24 via 192.168.2.1 - specify that you can reach the 192.168.2.0 network through the door or Gateway at one 192.168.2.1

ip route add default via 192.168.2.1 --> any request to any network outside of the existing network goes to this particular router
- 0.0.0.0 instead of default --> it means any IP destination. Both of these lines mean the same thing

For multiple routers in your network, one for the internet. Another for the internal private network. Then you will need to have two separate entries for each network. One entry for the internal private network and another entry with the default gateway for all other networks, including public networks. Ex: ip route add 192.168.1.0/24 via 192.168.2.2

By default in Linux packets are not forwarded from one interface to the next. This is this way for security reasons.

Whether a host can forward packets between interfaces is governed by a setting in the system at: <code>/proc/sys/net/ipv4/ip_forward</code>. By default, the value in this file is set to zero, meaning no forward. To persist the setting across reboots, modify the same value in /etc/sysctl.conf.
###### <strong style="color: #d79921">DNS Configuration</strong>

To associate an IP address with the name of a system, add to <code>/etc/hosts</code> file the ip and a name for the system.  Ex: 192.16.8.1.11 db

It can have as many names as the user wants for as many servers as the user wants in the /etc/hosts file.

Every time we reference another host by its name from host a through a pin command or SSH command or through any of the applications or tools within this system, it looks into its Etsy host file to find out the IP address of that host. Translating hostname to IP address this way is known as name resolution.

DNS Server --> single server that manages centrally all the entries for all the hosts

Every host has a DNS resolution configuration file at /etc/resolv.conf

> It's a file to configure the DNS server to be used for a host. Ex: search     mycompany.com prod.mycompany.com

So a system is able to use host name to IP mapping from the /etc/hosts file locally as well as from a remote DNS server. the host first looks in the local /etc/hosts file and then looks at the name server. The order is defined by an entry in the file at /etc/nsswitch.conf in the with hosts entry.

- www.google.com --> called a domain name and it is how IP is translate to names that we can remember on the public internet.
	- .com --> top level domain, represent the intent of the website
	- .goggle --> domain name assigned to Google
	- www --> sub domain, for external facing website

- nslookup --> tool to query a hostname from a DNS server. does not consider the entries in the /etc/hosts file
	- Ex: nslookup www.google.com

- dig --> another tool to test DNS name resolution
	- Ex: dig www.google.com
	- it returns more details in a similar form as is stored on the server
## **Version Control**
---
Source code management (or SCM) is the practice of tracking versions of source code as it is developed.

SCM tolls are also referred to as version control systems (VCSs)

SCM can be centralizaed or distributed. A centrlized SCM sotres code reopo and version history centrally. With distributed SCM,each developer has a local clone of code repo and version history.

Some of the most popular repository hosts are GitHub, GitLab, and BitBucket. Git is the current standard for version control software.

Gitflow --> metodo de versionamento e desenvolvimento

Git  
## **Virtualization**
---
#### <strong style="color:#689d6a">Virtual Machines</strong>

Check if virtualization is supported on Linux <span style="color: #3588E9">--></span> `grep -E --color 'vmx|svm' /proc/cpuinfo`
#### <strong style="color:#689d6a">Containers</strong>

An <span style="color: #d65d0e">image</span> <strong style="color: #b16286">is a package or a template</strong>, just like a VMM template that you might have worked with in the virtualization world. <strong style="color: #b16286">It is used to create one or more containers.</strong>

<span style="color: #d65d0e">Containers</span> <strong style="color: #b16286">are running instances of images</strong> that are isolated and have their own environments and set of processes.

A <span style="color: #d65d0e">container</span>, powered by the <span style="color: #d65d0e">containerization engine</span>, is a <strong style="color: #d79921">standard unit of software</strong> that encapsulates everything (applications code, runtime, system tools, system libraries) that programmers need to build, ship and run applications efficiently.

<span style="color: #3588E9">--></span> Containers solve the problem of making software portable so that applications can run on multiple platforms. This is possible because <strong>containers are platform-independent</strong> and can run on the cloud, desktop, and on-premises, and <strong>they are operating system-independent</strong>, which means they can run on Windows, Linux or Mac Os.

The container engine virtualizes the operating system and are responsible for running containers.

Unlike virtual machines, containers are not meant to host an operating system. Containers are meant to run a specific task or process, such as to host an instance of a web server or application server or a database.

> A container only leaves as long as the process inside it is alive. If the web service inside the container is stopped or crashed, then the container exits

- There are many popular container vendors today, which include: <span style="color:#98971a">Docker</span>, <span style="color:#98971a">Podman</span>, <span style="color:#98971a">LXC</span> and <span style="color:#98971a">Vagrant</span>.
	- <span style="color:#98971a">Docker</span> <span style="color: #3588E9">--></span> the most popular container platform today.
	- <span style="color:#98971a">Podman</span> <span style="color: #3588E9">--></span> daemon-less container engine that is more secure than Docker.
	- <span style="color:#98971a">LXC</span> <span style="color: #3588E9">--></span> preferred for data-intensive apps and operations.
	- <span style="color:#98971a">Vagrant</span> <span style="color: #3588E9">--></span> offers the highest levels of isolation on the running physical machine.

<span style="color:#98971a">busybox</span> <span style="color: #3588E9">--></span> it's a binary that contains many well know Unix tools like <span style="color: #98971a">awk</span>, <span style="color: #98971a">date</span>, <span style="color: #98971a">whoami</span>, <span style="color: #98971a">wget</span>.
##### <strong style="color:#d79921">Docker</strong>

Available since 2013, Docker Is an open platform (engine) written in Go, that allows to develop, deploy, test and run applications as containers. It uses Linux kernel's features to deliver functionality.

Docker isolates applications from infrastructure, including the hardware, operating systems and the container runtime. It uses the namespaces technology to provide an isolated workspace called "container" (containers are isolated from each other).

> The main purpose of Docker is to package and containerized applications and to ship them and to run them anywhere any time as many times is nedded.

Docker creates a set of namespaces for every container and each aspect runs in a separate namespace with access limited to that namespace.

<span style="color: #3588E9">--></span> <span style="color: #d65d0e">namespaces</span> is a <strong>feature of the Linux kernel</strong> that allows to provide complete network isolation to different processes on the system. It's similar in concept to what a <span style="color: #d65d0e">Hypervisor</span> does to provide the virtual resources to the Virtual Machine. They keep containers isolated until docker administrator allows containers to communicate over docker virtual network on the same host. With the namespaces isolation in Docker, operating systems and applications running in containers, feels like they have their own process tree.

namepsace isolation tecnique: Process ID namespaces

The processes running inside the container are in fact processes running on the underlying host. With process ID namespaces, each process can have multiple process IDs associated with it.

By default there is no restriction as to how much of a resource a container can use, and hence a container may end up utilizing all of the resources on the underlying host.

Docker primarily uses <span style="color: #d65d0e">cgroups</span> (control groups) to restrict the amount of hardware resources allocated to each container. This can be done by providing the --cpus option to the Docker run command. Example: docker run --cpus=.5ubuntu --> ensure that the container does not take up more than 50% of the host CPU at any given time. The same goes with memory: docker run --memory=100m ubuntu

Docker requires that virtualization to be enabled in the Bios, <span style="color: #d65d0e">VT-X</span> or <span style="color: #d65d0e">AMD-V</span>.

<span style="color: #3588E9">--></span> One of the goals of Docker is to make scripting distributed systems "easy".

- The <span style="color: #d65d0e">Docker Engine</span> which is the <strong style="color: #d79921">heart of Docker</strong>, is comprised of runtime and packing tools, and is required to be installed on the host that runs Docker. It's <strong>designed as client-server application</strong>, and it has these components: <span style="color:#98971a">Docker CLI</span> (docker client), <span style="color:#98971a">Dockerd</span> (docker daemon), <span style="color:#98971a">REST APIs</span>.
	- <span style="color:#98971a">Dockerd</span> <span style="color: #3588E9">--></span> it's the docker host server itself. The daemon listens for Docker API request or commands such as "docker run" and processes those commands. The daemon, is responsible for: build, run and distributes containers to the registry. Docker host includes and manages: images, containers, namespaces, networks, storage, plugins and add-on.
	- <span style="color:#98971a">Docker API</span> <span style="color: #3588E9">--></span> defines the interface that all programs use to talk to the daemon.
	- <span style="color:#98971a">Docker CLI</span> <span style="color: #3588E9">--></span> send instructions/commands to the Docker host server via command line interface (CLI) or through REST APIs. The Docker CLI can be used to communicate with local and remote host. The Docker CLI and the dockerd can run on the same system or connect the client to a remote docker daemon.
	- To use Docker CLI to work with remote docker engine, simply use the dash option (<code style="color:#689d6a">-H</code>) on the Docker command and specify the remote Docker engine address and a port <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker -H=[remote-docer-engine]:[port]</code> <strong>Example:</strong> <code style="color:#689d6a">docker -H=10.123.2.1:2375 run nginx</code>
	- <span style="color: #3588E9">--></span> <span style="color:#98971a">docker daemon</span> can also communicate with other daemons to manage Docker services.
	- The Docker engine also utilizes <span style="color: #d65d0e">cgroups</span> for isolation, which are used for controlling container resources, primarily around CPU and memory, they provide resource isolation. Cgroups in Docker are strict Kernel requirements, which means that they need to be compatible.
###### <strong style="color: #d79921">Docker Architecture</strong>
###### <strong style="color: #d79921">Docker Objects</strong>
###### <strong style="color: #d79921">Docker Commands</strong>
##### <strong style="color:#d79921">Vagrant</strong>
## **Container Orchestration**
---
<span style="color: #d65d0e">Container orchestration</span> is a process that automates the container life cycle of containerized applications, which includes: Deployment, Management, Scaling, Networking and Availability. It can be implemented on-premises, an on public, private, or multi-cloud environments. Container orchestration solves the problem of deploying multiple containers across many hosts.

<span style="color: #d65d0e">Container orchestration</span> <strong>features</strong><strong style="color:#3588E9"> :</strong> defines container images and registry, improves provisioning and deployment, secures network connectivity, ensures availability and performance, manages scalability and load balancing, resource allocation and scheduling, rolling updates and roll backs, health checks and automated error handling.

<span style="color: #d65d0e">Container orchestration</span> <strong>uses configuration files</strong> written in <span style="color:#98971a">YAML</span> or <span style="color:#98971a">JSON</span>. These files configure each container so it can find resources, establish a network, and store logs. Container orchestration manages the container's life-cycle based on specifications in the configuration file. This includes system parameters (like CPU and memory), and file parameters (like proximity and file metadata). And container orchestration supports scaling and enhances productivity, through automation.

- Some of the well-know <strong>container orchestration tools</strong> are: <span style="color:#98971a">Marathon</span>, <span style="color:#98971a">Hashicorp's Nomad</span>, [[ Docker Swarm ]] and [[ Kubernetes ]].
	- <span style="color:#98971a">Marathon</span> <span style="color: #3588E9">--></span> is a framework for Apache Mesos, and open-source cluster manager that was developed by the University of California at Berkeley. It allows the developer to scale container infrastructure by automating the bulk of management and monitoring tasks.
	- <span style="color:#98971a">Hashicorp's Nomad</span> <span style="color: #3588E9">--></span> is a free and open-source cluster management and scheduling tool that supports Docker and other standalone, virtualized, or containerized applications on all major operating systems across all infrastructure, whether on-premises or in the cloud.
	- <span style="color:#98971a">Docker Swarm</span> <span style="color: #3588E9">--></span> it's the cluster management and orchestration feature that was designed specifically to work with Docker Engine and other Docker tools. It's functionality comes from a separate project that Docker calls Swarmkit.
	- <span style="color:#98971a">Kubernetes</span> <span style="color: #3588E9">--></span> it's an open-source platform developed by Google, and it's the de facto standard for container orchestration. Kubernetes automates a host of container management tasks like: deployment, storage provisioning, load balancing and scaling, service discovery and "self-healing".

<span style="color: #3588E9">--></span> Container orchestration helps to meet business goals and increase profitability by using <span style="color: #d65d0e">automation</span>.

#### <strong style="color:#689d6a">Kubernetes</strong>

<span style="color:#98971a">Kubernetes</span> it's an open-source platform written in Go, which was developed by Google and maintained by the <span style="color: #d65d0e">Cloud Native Computing Foundation</span> (CNCF) that allows to manage containerized applications.  It can run in any kind of server, such as on-premise data centers, public, private and hybrid cloud.

<span style="color: #3588E9">--></span>  It's also kwon as "Kates" or K8s. Kubernetes is widely supported by leading cloud providers, many of whom now offer fully managed Kubernetes service.

[[ minikube ]]<span style="color: #3588E9"> --></span> is a software that allows developers to run a Kubernetes cluster on the local machine. It's a very useful tool that helps in the process of learning Kubernetes.

[[ Kubectl ]]<span style="color: #3588E9">--></span> is the Kubernetes command line interface (CLI), stands for Kube Command Tool Line. Its used to deploy and manage applications on a Kuberneters cluster to get cluster information, to get status of other nodes in the cluster, inspect and manage cluster resources, view logs, and more. Key commands types: Imperative commands, Imperative object configuration and Declarative object configuration.

Kubernetes uses <span style="color: #d65d0e">YAML files</span> as inputs for the <strong style="color: #b16286">creation of objects</strong> such as pods, replicas, deployments, services, etc. All of these follow a similar structure. A Kubernetes definition file <strong style="color: #b16286">always contains four top level fields</strong>: <span style="color: #d65d0e">apiVersion, kind, medata and spec.</span>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myaapp-pod
  labels:
    app: myapp
    tier: front-end
spec:
  containers: # List/Array 
    - name: nginx-container # dash indicates that this is the first item in the list
      image: nginx
```

> Note: A YAML file is used to represent data, which in Kubernetes is called Kubernetes manifests. Every manifest must define an API version to use.

- <span style="color: #d65d0e">apiVersion</span> <span style="color: #3588E9">--></span> the version of the Kubernetes API that will be used the object. <strong style="color: #d79921">Some possible values are</strong>: v1 for Pod and Service, apps/v1 for ReplicaSet and Deployment.
- <span style="color: #d65d0e">kind</span> <span style="color: #3588E9">--></span> refers to the type of the Kubernetes object that will be created
- <span style="color: #d65d0e">metadata</span> <span style="color: #3588E9">--></span> data about the object, like its name, labels, etc. It's in the form of a dictionary.
- <span style="color: #d65d0e">spec</span> <span style="color: #3588E9">--></span> provides additional information to Kubernetes pertaining to that object, it's going to be different for different objects. It's also a dictionary, so each property must be added under it

> For any Kubernetes definition file the spec definition defines what's inside the object that will be created.

<strong style="color: #d79921">Kubernetes Architecture</strong>
#### <strong style="color:#689d6a">Openshift</strong>

<span style="color: #d65d0e">Openshift</span> is an enterprise-ready Kubernetes container platform built for an open hybrid cloud strategy, developed by Red Hat.

Besides container orchestration, it provides additional tooling around the complete lifecycle of applications, from build, to CI/CD, to monitoring and logs.

Just like a Fedora distribution of Linux, OpenShift is a distribution of Kubernetes, building on its foundational capabilities.

<span style="color: #3588E9">--></span> OpenShift is used as an extension of Kubernetes to provide a more robust and comprehensive platform for containerized applications.

Openshift is a premiere platform for running micro services.

It orchestrates containerized workloads.

Microservices with OpenShift can easily integrate with serverless technologies.

Benefits: Enables simplified microservices development and deployment; Enables use of third-party software to fill gaps without requiring development of an entire solution.

A <strong style="color: #b16286">Build confguration file</strong> (BuildConfig) <strong style="color: #b16286">defines</strong> the <strong style="font-weight: 600">build strategy and input sources</strong>.

- Commonly <strong style="font-weight: 600">used</strong> <strong style="color: #b16286">Build strategies</strong> are: <span style="color: #98971a">Source to Image (S2I)</span>, <span style="color: #98971a">Docker</span> and Custom.
	- <span style="color: #98971a">Source to Image (S2I)</span>
		- Is a tool for building reproducible container images
		- Injects application source into a container image to produce a ready-to-run image
		- Eliminates using a Dockerfile
		- Go from Source to Image in one step
		- OpenShift includes predefined builder images
	- Custom
		- The developer must define and create his own builder image
		- Custom builder images are Docker images that contain logic to transform inputs ino expected outputs.
		- Custom builds are only available to cluster administrators

A build input source provides content for builds. The following build inputs can be used, listed in order of precedence: Inline Dockerfile definitions, Content extracted from existing images, Git repositories, Binary (or Local) inputs, Input secrets, and External artifacts.

><strong style="color: ">Note:</strong> multiple inputs can be combined into a single build. And, an inline Dockerfile takes precedence and overwrites any external Dockerfile.

An <span style="color: #d65d0e">ImageStream</span> is an abstraction for referencing container images within OpenShift. It continuouusly creates and updates containers images, but does contain actual image data but is merely a pointer <span style="color: #3588E9">--></span> points to images stored in internal and external registries, or to other ImageStreams.

A <strong style="font-weight: 600">single</strong> ImageStream can <strong style="font-weight: 600">consist of many different tags</strong> such as <strong style="color: #b16286">latest</strong>, <strong style="color: #b16286">dev</strong> and <strong style="color: #b16286">test</strong>. And each tag points to a certain image in a registry.

<span style="color: #3588E9">--></span> An ImageStream provides a trigger capability that automatically invokes builds and deployments when a new version of an image is available.

Red Hat Marktplace --> provides a central location to try, buy, deploy and manage software certified for OpenShift environments.

<strong style="color: #d79921">Openshift Architecture</strong>:

<strong style="color: #d79921">Types of triggers</strong>:

<strong style="color: #d79921">Operators</strong>:

<strong style="color: #d79921">Istio service mesh</strong>

<strong style="color: #d79921">Deploy microservices with OpenShift</strong>:
## **Cloud Computing**
---
It is a business model that allows the use of on-demand computing resources through network connections. In addition, Cloud computing enables efficient marketing of applications regardless of maintenance and cost.

NIST --> National Institute of Standards and Technology

NIST defines Cloud computing as a model for enabling convenient, on-demand network access to a shared pool of configurable computing resources that can be rapidly provisioned and released with minimal management effort or service provider interaction.

Examples of computer resources: networks , servers, storage applications, services.

- <strong style="color: white">Essentials characteristics:</strong>
	- on-demand self-service
	- broad network access
		- cloud computing resources can be access throw the network
		- public cloud services can be access form anywhere
	- resource pooling
		- save costs using a shared model (economies of scale)
		- multi-tenant model
	- rapid elasticity
		- increase and decrease resource as per demand
		- vertical scaling or horizontal scaling
		- add or decrease resources as per the number of users
	- measured service
		- pay for what you use or reserve as you use
		- utility model of billing (charged after the usage)
##### **<span style="color:#689d6a">Cloud Service Models</span>**

<span style="color: #d65d0e">Infrasctructure as a Service (IaaS)</span> is a set of compute, networking and storage resources that have been virtualized by a vendor so that a user can access and configure them. In the IaaS model, the cloud provider manages the physical resources: data centers, cooling, power, networkin & security, servers & storage

<span style="color: #d65d0e">Plataform as a service (PaaS)</span> takes advantage of all the virtualized resources from IaaS and then just abstracts them away, so the user doesn't have to worry about managing any of those virtualized resources. The provider manages the plataform infrastrcuture: operating system, development tools, databases.

<span style="color: #d65d0e">Software as a Service (SaaS)</span> is just software that the user don't have to install on his machine and he doesn't have to manually update. The cloud provider hosts and manages applications and data. The user for SaaS could be anyone. Example os SaaS: Gmail.

The <strong style="color: #b16286">Pyramid Metaphor</strong>, is meant to indicate that as we move down, we increasing complexity in terms of knowledge and management of infrastructure resources and we're increasing the ease of use.

<strong style="color: #b16286">Car Metaphor:</strong>
- IaaS = leasing
- PaaS = renting
- SaaS = taxi
##### **<span style="color:#689d6a">Deployment Models</span>**

Deployment models indicate where the infrastructure resides, who owns and manages it, and how cloud resources and services are made available to users. The four cloud deployment models include: Public Cloud, Private Cloud, Community Cloud and Hybrid Cloud.

###### <span style="color: #d79921">Public Cloud</span>

A public cloud is a <strong style="color: #b16286">virtualized multi-tenant architecture</strong> enabling tenants or users to share computing resources.

Users can access servers, storage, network, security and applications as services delivered by cloud service providers over the internet. Using web consoles and APIs, users can provision the resources and services they need.

The cloud provider owns, manages, provisions and maintains the infrastructure. The user pays for what he use within a certain period.

Public clouds offer significant cost savings in terms of Total Cost for Ownership (TCO) as the provider bears all the capital, operational, and maintenance expenses for the infrastructure and the facilities they are hosted in.

<strong style="color: white">Characteristics:</strong>
- Resources are distributed on an as-needed basis offered through a variety of subscription and pay-as-you-go models.
###### <span style="color: #d79921">Hybrid Cloud</span>

<strong style="color: #b16286">Cloud infrastructure provisioned for exclusive use</strong> by a single organization comprising multiple consumers, such as the business units within the organization. It may be owned, managed, and operated by the organization, a third party or some combination of them, and it may exist on or off premises.

Private cloud platforms can be implemented internally or externally.

When it is provisioned over a cloud providers infrastructure, it is owned, managed, and operated by the service provider. This external private cloud offering that resides on a cloud service providers infrastructure is called a <span style="color: #d65d0e">Virtual Private Cloud</span> or VPC.

>A <span style="color: #d65d0e">VPC</span> is a public cloud offering that lets an organization establish its own private and secure cloud-like computing environment in a logically isolated part of a shared public cloud.

A private cloud is a virtualized environment modeled to bring in the benefits of a public cloud platform without the perceived disadvantages of an open-end shared public platform.

<span style="color: #3588E9">--></span> Using a VPC, organizations can leverage the dynamic scalability, high availability, and lower cost of ownership of a public cloud, while having the infrastructure and security tailored to the organization's unique needs.

<span style="color: #d65d0e">cloud bursting</span> <span style="color: #3588E9">--></span> leveraging public cloud instances for a period of time, but returning to the private cloud when the surge is meet.

- <strong style="color: white">Benefits:</strong>
	- Controlled by internal IT
	- Reduced Costs
	- Better scalability --> through virtualization and cloud bursting
	- Controlled access & security
	- Greater agility
- <strong style="color: white">Use Cases:</strong>
	- modernizing in-house & legacy applications
	- build applications anywhere and move them without compromising security or compliance
	- full control over critical security and compliance issues within dedicated cloud
###### <span style="color: #d79921">Community Cloud</span>

“<strong style="color: #b16286">Cloud infrastructure that is provisioned for exclusive use by a specific community of consumers</strong> from organizations that have shared concerns (e.g., mission, security requirements, policy, and compliance considerations). It may be owned, managed, and operated by one or more of the organizations in the community, a third party, or some combination of them, and it may exist on or off premises.” (NIST definition)
##### **<span style="color:#689d6a">Cloud Infrastructure</span>**

The infrastructure layer is the foundation of the cloud. This layer consists of physical resources that are housed in Regions, Zones and Data Centers.

A cloud Region, is a geographic area or location where a Cloud provider’s infrastructure is clustered, and may have names like NA South or US East. The cloud Regions are isolated from each other so that if one Region was impacted by a natural disaster like an Earthquake, the Cloud operations in other Regions would keep running.

Each Cloud Region can have multiple Zones (or Availability Zones or AZ for short), which are typically distinct Data Centers with their own power, cooling and networking resources. These Zones can have names like DAL-09 or us-east-1. The isolation of zones improves the cloud’s overall fault tolerance, decreases latency, and avoids creating a single shared point of failure.

> A cloud Data center is a huge room or a warehouse containing cloud infrastructure.

Cloud providers offer several compute options – Virtual Servers, Bare Metal Servers, and “Serverless” computing resources. Most of the servers in a cloud datacenter run hypervisors to create virtual servers or virtual machines (also called VMs for short), that are software-based computers, based on virtualization technologies.

Virtual Machines or VMs are also known as Virtual Servers or Virtual Instances, or simply instances, depending on the cloud provider. When you create a virtual server in the cloud, you specify the Region and Zone or Data Center you want the server to be provisioned in and the Operating System you want on it.

> shared (that is, a multi-tenant) VMs or dedicated (that is, a single-tenant) VMs.
##### **<span style="color:#689d6a">Cloud Storage</span>**
## **Infrastructure as Code**
---
<span style="color: #d65d0e">Infrastructure as Code (IaC)</span> <span style="color: #3588E9">--></span> is the practice of describing infrastructure in textual format that is executable. The tools to configure infrastructure are called <span style="color: #d65d0e">Configuration Management Systems</span>, like <span style="color:#98971a">Ansible</span>, <span style="color:#98971a">Puppet</span> or <span style="color:#98971a">Chef</span>, that allows to describe the infrastructure as code and then creating that infrastructure and keep it in that way.

<span style="color: #3588E9">--></span> <strong style="color: #b16286">Server drift</strong> is a major source of failure. "Server are cattle not pets". Infrastructure is transient.

<span style="color: #d65d0e">Configuration Management Systems (CMS)</span> predated the IaC tools.

IaC tools can be either <strong>declarative</strong> or <strong>imperative</strong>. In a <strong style="color: #b16286">declarative approach</strong>, the desired state of the infrastructure resources to be provision. Tools that use this approach: [[ Terraform ]], <span style="color:#98971a">Puppet</span>, <span style="color:#98971a">SaltStack</span>, [[ CloudFormatiom ]] and [[ Ansible ]]. The <strong style="color: #b16286">imperative approach</strong>, requires to define the specific order of commands needed to achieve the sired state. The tools executes commands in that order. Tools that use imperative approach: <span style="color:#98971a">Chef</span> and <span style="color:#98971a">Ansible</span>.

IaC can be broadly classified into three types: Configuration Management, Server Templating and Provisioning Tools.

<span style="color: #d65d0e">Configuration Management</span> <span style="color: #3588E9">--></span> managing and operating system configuration including installed packages, device configurations, users, groups, ect. Tools like Ansible, Chef, Puppet and Salt Stack fall into this category, which are commonly used to install and manage software on existing infrastructure resources such as servers, databases, networking devices, etc...

> Note: Configuration management tools maintain a consistent and standard structure of code, and this makes it easier to manage and update it as needed. They're also designed to run on multiple remote resources at once.

<span style="color: #d65d0e">Proviosing</span> <span style="color: #3588E9">--></span> getting and setting the physical components to run specific applications. Tools like Terraform and CloudFormation are used to provision infrastructure components using a simple declarative code.

<span style="color: #d65d0e">Server Templating Tools</span> <span style="color: #3588E9">--></span> these are tools like Docker, Vagrant and Packer from Hashicorp that can be used to create a custom image of a virtual machine or a container. These images already contain all the required software and dependencies installed on them.

<strong style="color: white">Benefits</strong> of <span style="color: #d65d0e">IaC</span>: faster time to production, more efficient development, protection against staff churn, lower costs and improved use of developer time, and idempotente.

<span style="color: #d65d0e">In place update</span> <span style="color: #3588E9">--></span> use the same software upgrade lifecycle for each server using the same approach

> The underlying infrastructure remains the same, but the software and the configuration on each server are changed as part of the update <span style="color: #3588E9">--></span> <strong style="color: #d79921">Multable Infrastructure</strong>

<span style="color: #d65d0e">Configuration drift</span> <span style="color: #3588E9">--></span> when servers vary from one another, which can be in software configuration or operating system, etc.

Immutable infrastructure --> 

> With infrastructure as a code, immutability makes it easier to version the infrastructure and to roll back and roll forward between versions.
###### <span style="color:#689d6a">[[ Ansible ]]</span>

###### <span style="color:#689d6a">[[ Terraform ]]</span>

###### <span style="color:#689d6a">[[ CloudFormation ]]</span>
## **Serverless Architecture**
---
Serverless is an approach to computing that offloads responsibility for common infrastructure management tasks such as scaling, scheduling, patching, and provisioning application stacks to cloud providers

Serverless doesn't mean there are no servers, only that the management of the underlying physical or virtual servers is removed from their users

The serverless computing environment allocates resources as needed for the applications.

Attributes

Effectively, serverless abstracts the infrastructure away from developers, code is executed as individual functions, where each function runs inside a stateless container.

Some of the key serverless computing services today include IBM Cloud functions, which is based on Apache OpenWhisk, AWS Lambda and Microsoft Azure functions.

Applications that qualify for a serverless architecture include some of the following characteristics: short-running stateless functions, seconds or minutes, seasonal workloads with varying off peak and peaks, production volumetric data that shows too much idle time, event-based processing or asynchronous request processing for implementing use cases.

- Uses cases:
	- data and event processing
	- IoT
	- Microsservices
	- Mobile backends

Serverless is well suited to working with structured text, audio, image, and video data around tasks such as data enrichment, transformation, validation, and cleansing, DF processing, audio normalization, thumbnail generation, and video transcoding.

> Note: But for workloads characterized by long-running processes, managing a traditional server environment might be simpler and more cost effective.
##### **<span style="color:#689d6a">Serverless Computing</span>**

<span style="color: #d65d0e">serverless</span> <span style="color: #3588E9">--></span> "The concept of building and running applications that do not require server management" (CNCF).

Serverless computing offloads the responsibility of infrastructure management to cloud providers, enabling developers to focus on the application business logic.

<strong style="color: white">Charasterictics</strong>: Hostless, Elastic, Load balanced, Stateless, Event driven, Highly available, Usage-based/granular billing

- <strong style="color: white">Best practices</strong>:
	- Make each function perform only one action
	- Avoid function chaining
	- Limit dependencies on third-party libraries
---
- <strong style="color: #d65d0e">FaaS Model</strong>
	- Function as a Service (FaaS) --> cloud computing service that allows to execute code in reponse to events without complex infrastructure.
	- <strong style="color: white">Charasterictics</strong>: Creates applications as functions; Deploys on hybrid and on-premise; Stateless; Includess functions that execute in miliseconds and are instantaneously scalable; Lightweight and decoupled; Billed on consumption and execution.
	- <strong style="color: white">Benefits</strong>: divides server into functions, pay for what you use, inherent high availability.

<strong style="color: white">Self-managed FaaS</strong>:AWS Lamda, Google Cloud Functions, Azure Functions, IBM Cloud Functions, Openshift Cloud Functions(Red Hat).

<strong style="color: white">Managed FaaS providers</strong>:
- Fission <span style="color: #3588E9">--></span> framework for serverless function on Kubernetes
- Fn Project <span style="color: #3588E9">--></span> a container-native serverless platform
- Knative <span style="color: #3588E9">--></span> Kubernetes-based platform to build, deploy, and manage serverless workload
- OpenFass <span style="color: #3588E9">--></span> allows to turn any Linux or Windows process into a function
###### <span style="color: #d79921">Architecture concepts</span>

Abstracts infrastructure and software environment.

Code runs in a cloud platform.

Cloud provider manages the hardware and software setup, security, performance.

Billed only for usage

Developers only need to focus on applications and code in the form of functions.
###### <span style="color: #d79921">Constrains</span>

Unsuitable for long-running processes

Vendor lock-in risks

Cods starts

Latency unsuitable for time-critical apps

Security concerns

Complex monitoring and debugging

Language support dependency

Server optimization loss

No state persistence
###### <span style="color: #d79921">Stack components</span>

Fass, BaaS and API gateway.

Events ---> API Gateway ---{ requests }---> Functions ---> BaaS (File storage, Block Storage)

Events request can be webhooks from repositories such as Github and Docker Hub, and scheduled jobs. The functions then process these requests, and they are further directed (if necessary) toward the backend services. The output or response is then sent back to the client through the FaaS component and the API Gateway.
###### <span style="color: #d79921">The Serverless Framework</span>
###### <span style="color: #d79921">Serverless Reference Architecture</span>
###### <span style="color: #d79921">Build a serverless app with AWS Lambda</span>

1. Create a CodeCommit repository
2. Create an AWS Amplify resource
	1. choose "Home you web app"
	2. select "AWS CodeCommit"
	3. link the branch
3. Create the Lambda function
	1. define a test event
	2. create the reverse function
	3. chain both functions using StepFunctions
4. Create a state machine
	1. choose "design workflow visually"
	2. use "Express" option
5. Create an REST API with API Gateway resource
## **CI/CD**
---
<span style="color: #d65d0e">CI/CD</span> is an automated approach to developing and delivering software with <strong>repeatability and reliability</strong>. It's two separate and distinct process that happen right after other.

<span style="color: #d65d0e">Continuous Integration (CI)</span> <span style="color: #3588E9">--></span> is the process of continuously building, testing and integrations every developer change (code) into a repository by using short-lived branches. It ensures that the software continues to work properly after being pushed. The result is potentially deployable code. Examples of CI tools: Jenkins, Circle CI, Travis CI, GitHub Actions.

<strong>Benefits</strong> of <span style="color: #d65d0e">CI</span>:  faster reaction time to changes, reduced code integration risk, higher code quality, the code in version control works, master branch is always deployable.

<span style="color: #d65d0e">CI automation</span> <span style="color: #3588E9">--></span> build and test every pull request; use CI tools that monitor version control; tests should run after each build; never merge a pull request with failing tests.

<span style="color: #d65d0e">Continuous Delivery (CD)</span> <span style="color: #3588E9">--></span> is a series of practices designed to ensure that the code can be rapidly and safety deployed to production by delivering every change to a production-like environment. Is the next phase after CI, it prepares the code for release and automates the process that is required to deploy and build the application. Examples of CD tools: Spinnaker, Concourse CI, Gitlab, Travis CI, Tekton, GoCD, ArgoCD.

<strong>Benefits</strong> of <span style="color: #d65d0e">CD</span>:  automate software transportation through software development life-cycle (SDLC) stages, reduce deployment time, reduce costs, scale based on project size, deploy code automatically into each stage of SDLC.

<strong>Tasks</strong> in <span style="color: #d65d0e">CD pipeline</span>: security scanning, vulnerability scanning, secret scanning, Static Application Security Testing (SAST), Dynamic Application Security Testing (DAST).

<span style="color: #d65d0e">CI/CD pipeline</span> <span style="color: #3588E9">--></span> automated process that creates a pipeline of checks.

<span style="color: #d65d0e">Continuous Deployment</span> <span style="color: #3588E9">--></span> promote deployment to production (on-prem, public cloud, hybrid cloud), it can be a part of a Continuous Delivery pipeline.

<span style="color: #3588E9">--></span> Code needs to go through several stages of QA and testing to ensure what is delivered to production is fit for purpose.

<span style="color: #d65d0e">DevOps pipeline</span> <span style="color: #3588E9">--></span> workflow that automates software delivery. It is a series of interconnected steps that enable efficient and consistent execution of tasks such as building, testing, deploying, and releasing software.

<span style="color: #d65d0e">GitOps</span> <span style="color: #3588E9">--></span> operational framework that utilizes the best practices of DevOps.
## **Micro services**
---
Microsserviços é uma forma particular de projetar aplicações de software como suítes de serviços implantáveis de forma independente.

Surgiu como um movimento de neǵocio, devido ao desafio de como implantar software mais rapidamente.

O conceito de microsserviços se popularizou com a publicação do aritgo de Martin Flowlr em 105 - https://martinfowler.com/articles/microservices.html

Monolito não é um código ruim, é apenas um código que é implantado com um único bloco num ambiente de produção, isso muitas vezes dificulta para que esse processo seja rápido.

Razões para uso:

proteção modular --> arquitetura com baixo acoplamento e alta coesão

modelo conceitural --> https://github.com/dotnet/eShop

Com o modelo de microsservço, cada serviço será empacontado para poder ser implantadno de uma forma independente.

cada micro serviço opera de um forma independente, tipicamente ele é hospeado em um container como elemento de virtualização.

estrangular monolito --> mover de um monolito para uma arquitetura de microsserviços.

A adoção de uma arquitetura de microsserviços precisa fornecer autonoma técnica para os times.

Governança técnica descentralizada é abordagem recomendada para equipes operando com microsserviços.

Plataforma CNCF (Cloud Native Computing Foundation) --> fornece uma coridoria de mais de 1000 tecnologicas organziadas em domínios.

The Twelve-factor app methodology is suited for web apps, and it's frequently used with microservices.

The twelve factors can be grouped according to these phases of the software delivery lifecycle: <strong style="color: #d79921">Code</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Deploy</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Operate</strong>

A <strong style="color:#689d6a">Monolithic</strong> application has all or most of its functionality within a single process. And the application is managed in internal layers or libraries. The layers are tightly connected and dependent on each other.

<strong style="font-weight: 600">Benefits</strong> of Monolith: simple and less cross-cutting of features and functionalities

<strong style="font-weight: 600">Drawbacks</strong> of Monolith: with growth, complexity increases; less flexibility to adapt to new technology.

<span style="color: #d65d0e">Windows Forms Application</span> <span style="color: #3588E9">--></span> typical example of a Monolithic design.
#### **<span style="color:#d79921">Características</span>**
#### **<span style="color:#d79921">API Gateway</span>**
#### **<span style="color:#d79921">Padrões Arquiteturais</span>**
#### **<span style="color:#689d6a">Twelve-factor</span>**
#### **<span style="color:#689d6a">Microservices</span>**
#### **<span style="color:#689d6a">Microservices</span>**
#### **<span style="color:#689d6a">IBM Cloud Engine</span>**
## **Test and Behavior Driven Development**
---
<span style="color: #d65d0e">Automated testing</span> is critical for DevOps.

<span style="color: #d65d0e">Technical Debt</span> <span style="color: #3588E9">--></span> calculates in the evolution of the software code inspection the errors that are found, the time to correct these errors and the retests in the inspection tool. If the number of errors increases with each test, the technical debt increases.

<span style="color: #3588E9">--></span> the greater the test coverage, the lower the chance of failure.
##### **<span style="color:#689d6a">Functional Testing Tools</span>**

<span style="color: #98971a">Selenium</span> <span style="color: #3588E9">--></span> framework that has a set of open source, multi-platform tools, used to test web applications through the browser in an automated way.
- <strong style="color: #98971a">SELENIUM IDE:</strong> recommended for quick bug fix scripts
- <strong style="color: #98971a">WebDriver:</strong> create a suite of more robust automation and regression tests, recommended for when you have a collection of specific language associations to use in the browser
- <strong style="color: #98971a">SELENIUM Grid:</strong> more distributed testing process, requires testing in a different browser and environment

<span style="color: #98971a">Appium</span> <span style="color: #3588E9">--></span> free framework for self-automation of software testing that works in web and mobile applications. HTTP server that runs on NodeJS and creates and manipulates various web servers sections for different platforms, such as iOS and Android. Can automate desktop testing.

>[!info]
> The tool depends on the company context
##### **<span style="color:#689d6a">Test driven development (TDD)</span>**

It was created by Kent Black and it is a methodology for developing and writing code.

<span style="color: #3588E9">--></span> It's lower level of testing

Focuses on how the system work from the inside out <span style="color: #3588E9">--></span> testing the functions inside the system

In TDD, the test cases drive the development.  The test cases are written based on the application's requirements <span style="color: #3588E9">--></span> tests are written first then the code is written to make the tests pass.

The requirements describe how the application should behave, and then the test cases verify that the application behaves that way.

Writing test cases first keeps the developer focused on how the code should behave before to write it.

TDD yields higher quality code.

<strong style="color: white">Basic TDD workflow</strong>
- <span style="color: #c6554f">RED (Fail)</span> --> <span style="color: #689d6a">GREEN (Pass)</span> --> <span style="color: #3588E9">Refactor</span>
	- <span style="color: #c6554f">RED</span> --> Write a test case that fails
	- <span style="color: #689d6a">GREEN</span> --> Write code to make it pas
	- <span style="color: #3588E9">Refactor</span> --> Improve code quality

<strong style="color: white">TDD importance for DevOps</strong>
- It saves time when developing
- It allows to code faster and with more confidence
- In ensures that the code is working as expected
- It ensures that future changes don't break the code

In order to create a DevOps CI/CD pipeline, all testing must be automated <span style="color: #3588E9">--></span> test automation must be done from the moment a stable version of the system is available.

<span style="color: #d65d0e">Test coverage</span> <span style="color: #3588E9">--></span> the percentage of lines of code that are executed during all of the tests.
- test coverage reports can reveal which lines of code were not tested
- even with 100% test coverage the code can still have bugs.
- 100% test coverage only means that every line of code has been tested with some known good data

>[!info]
>high test coverage is valuable for development because, it increases likelihood that the code works as expected

<span style="color: #d65d0e">Factories</span> and <span style="color: #d65d0e">fakes</span> are useful for creating and maintaining a large amount of test data. Factories generate fakes with realistic test data. Fakes behave like real objects during testing.
- the <span style="color: #98971a">Meta</span> class inside the factory is used to determine the attributes to use for generating data.
- to test fakes generated by a factory, just test fakes like real objects (data)
###### <strong style="color: #d79921">Tools for TDD</strong>

<span style="color: #98971a">xUnit series</span>: Junit for Java, PyUnit for Pythin, NUnit for .Net, Enbunit for C/C++

<span style="color: #3588E9">--></span> All versions of xUnit share common syntax.

Some other notable testing frameworks: Jasmine for JavaScript, Mocha for Node.js and Simpletest for PHP.

>[!hint]
>Look for a testing framework for the language that is being used.

<span style="color: #98971a">Pytest</span> <span style="color: #3588E9">--></span> you can have nearly infinite number of setups and tear downs.

<span style="color: #98971a">Doctest</span> <span style="color: #3588E9">--></span> actually allows you to write your test in the doc-strings or your comments of your code
- limited and doesn’t really scale for complex and highly interactive code

<span style="color: #98971a">Rspec</span> <span style="color: #3588E9">--></span> extremely popular framework for Ruby that is also available in Python

<span style="color: #98971a">PyUnit</span> <span style="color: #3588E9">--></span> also known as the unittest package
- is built into Python
- best to used in all the tests folder
- returns a report about the tests
- <strong style="color: white">Usage:</strong>  <code style="color: #00d2d2">$ python -m unittest discover</code> | "-v" option <span style="color: #3588E9">--></span> stands for verbose mode

<span style="color: #98971a">Nose</span> <span style="color: #3588E9">--></span> is a test runner, while PyUnit has its own test runner
- allows to add color and formatting and other test output <span style="color: #3588E9">--></span> get the Red/Green/Refactor
- provides much more detailed useful report
- supports code coverage --> the percentage of code that gets executed when you run automated testing
- The coverage tool also has options to report on the lines of code that have not been executed during a test run
- nosetests <span style="color: #3588E9">--></span> nose runner
- <strong style="color: white">Usage:</strong>
	- <code><span  style="color: #00d2d2">$ pip</span> install nose</code>
	- <code><span  style="color: #00d2d2">$ pip</span> install pynocchio</code>
	- <code><span  style="color: #00d2d2">$ nosetests</span> -v --with-spec --spec-color</code>
	- <code><span  style="color: #00d2d2">$ pip</span> install coverage</code>
	- <code><span  style="color: #00d2d2">$ python</span> install coverage</code>
	- <code><span  style="color: #00d2d2">nosetests</span> -v --with-spec --spec-color --with-coverage --cover-erase</code>
		- <span style="color: #00d2d2">--with-spec</span> <span style="color: #3588E9">--></span> show a title
		- <span style="color: #00d2d2">coverage report -m</span> <span style="color: #3588E9">--></span> run a report on the missing lines of code
		- <span style="color: #00d2d2">--cover-erase</span> <span style="color: #3588E9">--></span> erase the coverage to get the true coverage

The best way to use Nose it is through a configuration file with the necessary parameters (flags) <span style="color: #3588E9">--></span> <span style="color:">setup.cfg</span>

>[!example] setup.cfg
><span>[nosetest]</span>
>verbosity=2
>with-spec=1
>spec-color=1
>cover-erase=1
>cover-package=triangle
>
><span>[coverage:report]</span>
>show_missing = True
###### <strong style="color: #d79921">Test Assertions</strong>

A <span style="color: #d65d0e">test assertion</span> is a <strong style="color: #b16286">statement that evaluates to either True or False</strong>

Assertions are used as checks to determine if the results of the test have passed or failed <span style="color: #3588E9">--></span> True means passed and False means failed

Raise an exception if False, marking the test as failed

<strong style="color: #b16286">Assertions are native to Python</strong>, and one can be made using the assert() function

```python
answer = sum(2, 3)
assert(answer == 5)
```

Nicer way to make assertions: using additional asserts that Test Case provides.

To write test assertions: think about the functionality, how should it work, and then execute something and then write an assertion that what you executed actually did the behavior that you expected.

"happy paths" --> scenarios where everything should go as planned
- verify that a function returns positive outcomes when expected.

"sad paths" --> scenarios where we expect something to go wrong
- verify that a function responds to exceptions appropriately and without breaking

<strong style="color: #98971a">Common assertions for PyUnit</strong>
###### <strong style="color: #d79921">Test fixtures</strong>

Test fixtures are used to establish an initial known state before and after running test.

They run tests in isolation, and ensure repeatable results.

Test fixtures are helpful for many testing situations.

Test fixtures operate at three levels of specificity: module, test case, and test.

<strong style="color: white">Uses Cases:</strong>
- Preparation of input data
- Setup/creation of fake or mock objects
- Loading a database with a known set of data
- Copying a specific known set of files

<span style="color: #3588E9">--></span> Anything needed to do, to set up the proper environment to run the tests can be accomplished with test fixtures.

- <strong style="color: white">Test fixtures in PyUnit</strong>
	- setUpModule() <span style="color: #3588E9">--></span> runs once before the entiry python module. If the module has multiple TestCase classes it runs once before any of those classes run
	- tearDownModule() <span style="color: #3588E9">--></span> runs once at the end of the module, after all the tests have run. It is used to clean up once after all the test have been completed
	- testCaseClass() it can have a class method called setUpClass() that will run once before all the tests in that class
	- tearDownClass() <span style="color: #3588E9">--></span> is another class level method that will run once after all the tests in that class have run
	- setUp() <span style="color: #3588E9">--></span>  will run before each test
	- tearDown() <span style="color: #3588E9">--></span> will run after each test
	- <span style="color: #3588E9">--></span> setUp() and tearDown() are at the instance level.

Sometimes its needed to load a known set of data before run tests

>[!example]
>tests
>|
>|---- test_models.py
>|---- test_routes.py
>|---- fixtures <span style="color: #3588E9">--></span> signals to devs that the files inside have to do with test fixtures
>|---- | ---- account_data.json

Using fixtures to load test data is very handy especially when the data is complex and it would have been difficult to otherwise create it

Test fixtures will run before and after either all of the tests or individual tests or an entire test module. And it's a great place to put in hooks to initialize databases, initialize data files and then that type of thing.
###### <strong style="color: #d79921">Mocking</strong>

<span style="color: #d65d0e">mocking</span> <span style="color: #3588E9">--></span> process for creating objects that mimic the behavior of real objects

Mock should be used when:
- have an external device that is not under test
- need to change the behavior of a dependent system under test
- don't have a remote connection to another component
- to isolate tests from a remote component or external system

<strong style="color: white">Methods:</strong>
- <span style="color: #d65d0e">Patch</span> <span style="color: #3588E9">--></span> to change the behavior of function call 
	- to simulate error conditions and control what is returned from a call to any function <span style="color: #3588E9">--></span> including third-party libraries
	- useful when the function calls an external system that we don't control
	- useful to simulate error conditions that can be caused while under test
- <span style="color: #d65d0e">Mock object</span> <span style="color: #3588E9">--></span> simulates the behavior of real object
	- best used when it needs an entire object that behaves like another object
	- mock objects in unittest: 
		- <span style="color: #98971a">Mock</span>
		- <span style="color: #98971a">MagicMock</span> <span style="color: #3588E9">--></span> implements all of the magic functions in Python
		- with magic functions, mock objects can be used in place of containers or other objects that implement the Python protocols
	- to make the objects mimic a given real object, specify the real object's name as the spec parameter

<strong style="color: white">Patching techniques -  Python's mock library</strong>
- <span style="color: #98971a">Patching a function's return value</span>
	- <strong style="color: #3588e9">Useful for:</strong>
		- testing error handlers
		- controlling data returned from a function call  
- <span style="color: #98971a">Replacing a function with another function</span> <span style="color: #3588E9">--></span> called side effect
##### **<span style="color:#689d6a">Behaviour driven development (BDD)</span>**

Criado por Dan North, quem criou o primeiro framework BDD para java <span style="color: #3588E9">--></span> Jbehave; Rbehave para Rub e RSpec.

Focuses on the behavior of the system as observed from the consumer's perspective. Works great for integration testing, to see if all the components are behaving together.

BDD describes behaviors in a single syntax that domain experts, testers, developers, and customers can easily understand. This improves communication across the team.

It's higher level of testing. It tests the behavior of the system from the outside in and considers how the system should behave. The system behavior is observed, just like a user of the system would experience it.

BDD is usually performed at the integration, system, or acceptance test levels. At those levels, enough of the system is running that its behavior can be evaluated.

<strong style="color: white">Benefits of BDD language:</strong>
- uses a single syntax that everyone can easily understand
- notations are closes to everyday language than TDD and have a shallower learning curve
- the specification describes how the system should behave in a situation
- tools afford the automatic generation of technical documentation from specifications
- test can be generated to confirm the behavior was implemented

The most commonly used syntax in BDD is called <span style="color: #d65d0e">Gherkin</span>, which is used to document the behavior of a system. It got the name Gherkin because one of the first BDD tools was called Cucumber. 

Gherkin is an <strong style="color: #b16286">easy-to-read natural language syntax</strong> (both developers and stakeholders can easily understand) that uses a familiar Given, When, Then.

- <strong style="color: #d79921">Gherkin Syntax</strong>
	- <span style="color: #98971a">Given</span> <span style="color: #3588E9">--></span> set of preconditions
		- conditions required to put the system into the state needed to perform the tests
	- <span style="color: #98971a">When</span> <span style="color: #3588E9">--></span> an event occurs 
		- actions that the user takes to interact with the system under test
	- <span style="color: #98971a">Then</span> <span style="color: #3588E9">--></span> some testable outcome is observed
		- expected outcome of the actions the the user performs
	- <span style="color: #98971a">And</span> <span style="color: #3588E9">--></span> used for continuations
		- always take on the meaning of the previous Given, When, or Then that comes before it
	- <span style="color: #98971a">But</span> <span style="color: #3588E9">--></span> for steps that state what should not occur
		- extra option to improve readability

<strong style="color: white">BDD workflow</strong>
- Explore the problem domain and collaborate to produce concrete examples
- Use <span style="color: #98971a">Behave</span> (test runner) to run those example as automated tests
	- it parses the Gherkin syntax and looks for test steps that it can use to confirm that the system behaves as expected
- Behave tells which examples are implemented and working
- We now have one document that acts as both the specification and the tests for the software
	- is a living document checked into the source control system, and test cases can be run against it <span style="color: #3588E9">--></span> documentation drives the system

<strong style="color: white">BDD tools</strong>
- <span style="color: #98971a">Cucumber</span>
	- has free and paid versions
	- uses a plain text format 
	- uses Gherkin syntax
	- supports: Ruby, Java, .NET, Web apps
- <span style="color: #98971a">Behave</span>
	- supports Python
	- uses a plain text format 
	- supports: 
		- Gherkin features
		- Python steps
		- Environmental controls
	- also has a Java version --> JBehave
- <span style="color: #98971a">Concordion</span>
	- open source tool for Java
	- uses normal language in paragraphs
	- ported to other languages including:
		- C# (Concordion .NET)
		- Python (PyConcordion)
		- Ruby (Ruby-Concordion)
###### <span style="color: #d79921">BDD Specification</span>

A specification is made up of one or more <span style="color: #d65d0e">features</span>, which <strong style="color: #b16286">represent user stories</strong>. You can have as many features as needed.

Each can be placed in its own specification file, but  it could certainly place them all 
in one file or group.

>[!example] Feature Syntax
> Feature: `<title>`
> 
> As a `<role>`
> I want `<functionality>`
> So that `<benefit>`

Each feature contains one or more concrete examples, or <span style="color: #d65d0e">scenarios</span>. A scenario is a <strong style="color: #b16286">situation that describes a single behavior</strong> of a feature, and the syntax Given, When, Then is used to write that description. 

Each scenario formulates a complete test case for the behavior. Many scenarios can be written to describe the various behaviors of the feature.

>[!example] Retail BDD example
>Feature: Returns go to stock
>
><strong style="color: #3588E9">As a</strong> store owner 
><strong style="color: #3588E9">I want</strong> to add items back to stock when they're returned
><strong style="color: #3588E9">So that</strong> I can keep track of stock
>
>Scenario 1: Refunded items should be returned to stock
><strong style="color: #3588E9">Given</strong> that a customer previously bought a black sweater from me
><strong style="color: #3588E9">And</strong> I have three black sweaters in stock
><strong style="color: #3588E9">When</strong> they return the black sweater for a refund
><strong style="color: #3588E9">Then</strong> I should have four black sweaters in stock
###### <span style="color: #98971a">Behave</span>

Behave looks for a folder named `features`. All of the files that control Behave must be under the top-level features folder.

Inside the features folder, Behave looks for files with an extension of `.feature`. Those files can have any name. The features folder also contains a subfolder called “steps.”

Inside the steps folder is a collection of Python files that have the steps that match  the Gherkin statements in the feature files. Most people use `_steps` in the name to signify that they’re steps files.

``` 
.
|___ features
     |___ some.feature
     |___ some_other.feature 
     |___ steps
          |___ web_steps.py
          |___ load_steps.py
```

Best practice suggests to place all of the generic steps that manipulate the web interface, regardless of application, into a file called `web_steps.py`.

Additional Python files containing steps,can be stored in the steps folder as well.  Behave will load all of the steps in the Python files in this folder.

>[!note]
>There’s not a one-to-one correlation between the feature files and the step files.

<strong style="color: white">Using Behave</strong>
1. Set up the folder structure 
2. Run Behave --> `$ behave`
	1. Read feature files
	2. Reads through each scenario
	3. Processes each step's keyword and test string pair
	4. Finds a matching pair in the steps file
	5. Executes those functions

Behave only looks for the Python decorators that wrap the functions, it uses string matching to find the Python steps to execute. When Behave begins to execute, it scans the feature file to find the first scenario.

`@given('some known state')`
`@when('some action is taken')`

The steps do not have to be in any particular order in the steps file. Behave will find them regardless of the order of appearance in the file.

Step implementations:

start by importing the when and then decorators from Behave. Since you don’t use the Given keyword in the feature file, you don’t need to import  the Given keyword decorator here.

```python
from behave import when, then

# invoke the function that follows 'when'
@when('I visit the "Home Page"')
def step_impl(context):
	""" Make a call to the base URL """
	context.driver.get(context_base_url)

@then('I should see "Welcome to the Pet Shop" in the title')
def step_impl(context):
	""" Check the title for the Welcome Message """
	assert "Welcome to the Pet Shop" in context.driver.title

@then('I should not see "404 Not Found"')
def step_impl(context):
	""" Check the body for error message """
	element = context.driver.find_element(By.TAG_NAME, 'body')
	assert "404 Not Found" not in element.text
```

<code style="color: #689d6a">context</code> <span style="color: #3588E9">--></span> variable passed into every step definition
- exists for the entire feature file
- is useful for passing information between steps

<span style="color: #d65d0e">variable substitution</span> <span style="color: #3588E9">--></span> makes the steps more generic
- minimizes the number of steps
- leads to greater reuse
- Ex: `@when('I copy the "{variable_name}" field')`

```python
@when('I copy the "{element_name}" field')
def step_impl(context, element_name):
	element_id = element_name.lower().replace(' ', '_')
	element = context.driver.find_element(By.ID, element_id)
	context.clipboard = element.get_atribute('value')

@when('I paste the "{element_name}" field')
def step_impl(context, element_name):
	element_id = element_name.lower().replace(' ', '_')
	element = context.driver.find_element(By.ID, element_id)
	element.clear() # clears the element
	element.send_keys(context.clipboard)
```

In BDD, each step is just one part of a test case; it’s not an entire test case itself

Step workflow
1. Write a step for each Gherkin statement
2. Implement the step in Python
3. Repeat

<span style="color: #d65d0e">test fixtures</span> <span style="color: #3588E9">--></span> functions to control the test execution environment, which are declared in a file called `environment.py`.
- `before_all(context)` --> code that executes before all the features 
	- ideal for setting up web drivers from tools like Selenium
	- selenium drivers, allows use a real browser to perform the testing
	- ideal for establishing the context values that all the steps can access and for shutting down any drivers after Behave processes all the features
- `after_all(context)`
- `before_feature(context, feature)` --> run before each feature
	- every feature pass-in is an instance of the feature class
	- this set can be ideal for setting up a clean environment before and after each feature runs
- after_feature()
- before_scenario(context, scenario) --> The scenario is passed in as an instance of the scenario class
	-  you could have even more granular control over each scenario execution environmen
- after_scenario()
- before_step(context, step) --> The step passed in is an instance of the step class
- after_step()
- before_tag(context, tag) --> 
	- You can tag sections of your feature file with a name and then these functions run before and after the section tag with a given name. Behave invokes tags by the order they're found in the feature file
- after_tag()

```python
from os import getenv
from selenium import webdriver

WAIT_SECONDS = int('WAIT_SECONDS', '60')
BASE_URL = getenv('BASE_URL', 'http://localhost:8080')

def before_all(context):
	""" Executed onde before all test """
	context.base_url = BASE_URL
	context.wait_seconds = WAIT_SECONDS
```

<strong style="color: white">Tips</strong>
- strive for consistency
- consider the user experience
- build in cues that signal that the system has responded to the request

>[!example]
>Feature: Search for pets by category
>
>As a customer
>I need to be able to search for a pet category
>So that I can only see the category of pet I"m interested in buying
>
>Background:
>
>	Given the following pets
>		| name      | category  | available |
>		| Fido      | dog       | True      |
>		| Kitty     | cat       | True      |
>		| Leo       | lion      | False     |
>
>Scenario: Search for dogs
> - Given I am on the "Home Page"
> - When I set the "Category" for "dog"
> - And I click the "Search" button
> - Then I should see the message “Success”
> - And I should see “Fido” in the results
> - But I should not see “Kitty” in the results
> - And I should not see “Leo” in the results

Use the `Background:` keyword, along with the `Given` keyword, to define the initial state as a table of data.

The data must be loaded manually. The data is ins `context.table`.

```python
@given('the following pets')
def step_ipml()
""" Load """
# Return every row in the table as a dictinary
for row in context.table:
	payload = {
		"name": row['name'],
		"category": row['category'],
		"available": row['available'] in ['True', 'true', '1']
	}
	# make an HTTP request to the server’s REST API
	context.resp = request.post(
		f"{context.base_url}/pets",
		json=payload # send the Python dict as a JSON string
	)
	assert context.resp.status_code is 201
```
###### <span style="color: #98971a">Selenium</span>

Selenium is a collection of tools for automating web browser activity

At its core, Selenium is a WebDriver, an interface to write instruction sets that you could run interchangeably across popular browsers like Chrome, Firefox, Safari, and Edge.

With only a few lines of code it interacts with browsers just like real users would. You could enter data into fields, read data back from fields, click links, click buttons, everything a real user can do.

Works perfectly for integration testing of multiple microservices that share a common user interface.

Iniitialize Selenium
1. Ensure the web rower is installed
2. Instantiate the driver

To use Selenium, you must first tell it which element on the HTML page you want to interact with. Selenium can find elements by Class name, CSS selector,  ID, name, XPath, link text, partial links text, tag names.

Selenium for Python has function calls for each of these selectors.
- Ex: `find_element(By.ID, element_id)`

```python
def step_impl(context, text_string):
	""" Get the value of a test filed """
	element = context.driver.find_element(By.ID, 'customer_id')

	# specify what happens when Selenium finds this element
	assert text_string in element.get_attribute('value')

	element.clear()
	# type the text string into the input field
	element.send_keys(text_string)
```

experience latency when testing in a web UI, so you need to wait for something to appear. Luckily, the web driver has a web driver wait function to do just that.

```python
WAIT_SECONDS = 60

def step_impl(context, text_string):
	""" Wait for the value of a test field """
	found = WebDriverWait(context.driver, WAIT_SECONDS).until(
		expected_conditions.text_to_be_present_in_element_value (
			(BY.ID, 'customer_id'),
			test_string
		)
	)
	expect(found).to_be(TRUE)
```

very helpful when making calls to remote applications that may involve latency
##### **<span style="color:#689d6a">Acceptance Test-Driven Development (ATDD)</span>**

It is carried out collaboratively with a survey of all requirements and acceptance criteria, for each story in addition to possible scenarios <span style="color: #3588E9">--></span> it <strong style="color: #b16286">must involve the entire team</strong>.

In this methodology meetings take place, requirements are identified based on information gathering and the customer problem.

<span style="color: #3588E9">--></span> ATTD explores all possible scenarios of business criteria.

It uses the <span style="color: #d65d0e">Gherkin syntax</span>.

It is possible with <span style="color: #98971a">cucumber</span> or <span style="color: #98971a">JUnit</span> to automate the ATDD process.
## **Monitoring and Observability**
#### **<span style="color:#689d6a">Monitoring</span>**
---
Monitoring refers to the process of collecting data about a system or application over time, typically using metrics or logs.

Monitoring is for the identification, measurement, and evaluation of applications.

> Monitoring is a routine, ongoing process, and it is an operational-level activity. It’s usually performed by developers and their teams.

Monitoring typically involves looking at predefined metrics or logs over time to detect problems or anomalies.

Through monitoring, application management tools can identify, measure, and evaluate how well an application is working <span style="color: #3588E9">--></span> helps keeps an app running and improves performance.

It also allows the <strong style="color: #b16286">tracking of important data</strong>, such as application availability, occurrences of issues and bugs, resources being used, and changes that might alter the user experience.

Application monitoring can be accomplished by using specific tools for monitoring apps or by collecting and analyzing logs using log management tools.

<span style="color: #3588E9">--></span> Monitoring <strong style="color: #b16286">ensures that an application is healthy</strong> and responds to all requests accurately and quickly.

Application performance monitoring tools continuously <strong style="color: #b16286">monitor performance and send alerts</strong> when an application is <strong style="color: #d79921">not performing</strong> as it should.

<span style="color: #d65d0e">Real-time monitoring</span> determines the scope of usage.

Monitoring can also <strong style="color: #b16286">reduce costs</strong> due to unavailability of the app or poor performance.

It can <strong style="color: #b16286">ensure that applications are safe</strong> from any unwelcome or unwanted intrusions.

<span style="color: #d65d0e">Anomaly detection</span> <span style="color: #3588E9">--></span> observe simple threshold issues, which helps advance machine learning pattern recognition (critical part of monitoring).

<span style="color: #d65d0e">Distributed tracing</span> <span style="color: #3588E9">--></span> detect the origins of errors across multiple nodes.

<span style="color: #d65d0e">Dependency and flow mapping</span> <span style="color: #3588E9">--></span> way of monitoring apps with a visual representation of how information travels between services.

The effectiveness of the monitoring solution is based on how it’s implemented.
##### <span style="color:#d79921">Evaluation</span>

Evaluations are long-term processes that may happen only a few times.

> Note: is a business-level activity, and it is usually performed by others not involved in developing the application (managers, supervisors, or external independent parties).

Is an assessment of whether a solution meets its stated goals.

It's determined at the design stage or when the solution was implemented

Anticipated and unanticipated outcomes

Can show how useful an app is and how sustainable and profitable it is.

Is an important part of the <strong style="color: #b16286">monitoring process</strong><ul><li>Monitoring -- Performance -- Solutions</li></ul>
- <strong style="color: white">Critical questions</strong>
	- Easy of deployment
	- Statistics and metrics
	- Alerts and notifications
	- Deployment location
- <strong style="color: white">Benefits</strong>
	- assessment of solutions
	- improves effectiveness
	- meets standards
##### <span style="color:#d79921">Types of monitoring</span>

- <span style="color: #98971a">System monitoring</span>
	- --> it's designed to provide developers with information about the availability of their software.
	- it provides information about system uptime and the performance of applications
	- includes server management infrastructure monitoring and management
	- also includes network monitoring and management
	- uptime or availability monitoring --> checks application's status
- <span style="color: #98971a">Dependency monitoring</span>
- <span style="color: #98971a">Integrations moniroting</span>
- <span style="color: #98971a">Web performance monitoring</span>
- <span style="color: #98971a">Business Activity Monitoring (BAM)</span>
- <span style="color: #98971a">Application Performance Monitoring (APM)</span>
- <span style="color: #98971a">Real User Moniroting (RUM)</span>
- <span style="color: #98971a">Security monitoring</span>
##### <span style="color:#d79921">Golden signals</span>

<strong style="color: #b16286">Four most important metrics</strong> for measuring the health of a service or systems <span style="color: #3588E9">--></span> Troubleshooting systems, alerting about incidents, aiding in planning.
- <span style="color: #98971a">Latency</span> <span style="color: #3588E9">--></span> measures the time between when a request is sent and when a request is completed
	- --> successful and failed requests both have latency!!
	- longer latency times --> may indicate slower connection errors
	- include error latencies along with all other latencies
- <span style="color: #98971a">Traffic</span> <span style="color: #3588E9">--></span> indicates demand for service
	- helps fine-tune user experience
	- show storage system traffics
	- measures web app traffic
	- viewable by page or resource
- <span style="color: #98971a">Errors</span> <span style="color: #3588E9">--></span> proactively fix errors
	- fix failed requests and requests completed incorrectly
	- define critical errors
	- understand the system's health
	- track erros: servers, client, incorrect content
- <span style="color: #98971a">Saturation</span> <span style="color: #3588E9">--></span> measure the percentage of use of a system
	- Ex: Memory and CPU resources usage
	- --> optimize the services
	- set a utilization target
	- recognize latency and saturation indicators
##### <span style="color:#d79921">Components of monitoring</span>
##### <span style="color:#d79921">Synthetic Monitoring (SM)</span>
##### <span style="color:#d79921">Application Monitoring</span>
##### <span style="color:#d79921">Visualization</span>
##### <span style="color:#d79921">Alerting</span>
##### <span style="color:#98971a">Prometheus</span>
##### <span style="color:#98971a">Grafana</span>
#### **<span style="color:#689d6a">Logging</span>**
---
Is a series of messages from an application that provide a recorded log of the application's activities.

Log messages provide important information for developers when debugging an application and for system administrators maintaining applications in production.

An application log contains information about events that have occurred within a software application. Includes erros, events, and warnings.

Cloud-native applications treat logs as event streams.

An application log reveals message flow issues and app problems. It can also contain information about user and system actions that have occurred.

Logs are your first level of understanding of what your application is doing in production. Don't skimp on logging!!

Logged events: messages and warnings, application messages, transaction flow events, low disk space, completed operations, error events, success audits, failure audits.

Obs: Identifying what information should be collected and how it will be used is an important part of logging.

--> Like applications, logs must be designed, implemented, and tested.
##### **<span style="color: #d79921">Why use it</span>**

##### **<span style="color: #d79921">Log monitoring tools</span>**

##### **<span style="color: #d79921">Logging Tools</span>**

##### **<span style="color: #d79921">Types of applications logs</span>**

##### **<span style="color: #d79921">Log Storage</span>**
#### <span style="color:#689d6a">Observability</span>
---
Observability is a term used in engineering and computer science to describe the ability to understand the internal state of a system using its external output

It refers to the extent to which we can infer what's happening within a system by examining its external behavior

An observable system is one that provides sufficient information about its internal workings to allow operators and developers to diagnose issues and understand how it behaves under different circumstances.

The goal of observability is to enable faster identification and resolution of issues, ultimately leading to more reliable and efficient systems.

It involves not just collecting data but also analyzing in real time and using it to gain deeper insights into how a system is functioning.

It allows teams to quickly identify and resolve issues in complex systems by providing context rich information that helps them understand how the different parts of the system are interacting

is a proactive approach --> checking real-time system behavior, with minimal predefinition of what to look for.

It provides visibility into the internal workings of a system, allowing engineers to understand how it operates and diagnose issues more efficiently.

<strong style="color: white">Benefits</strong>
- Application performance monitoring
	- identify root causes of application performance issues
- Infrastructure and cloud monitoring
	- Improve application up time and performance
	- cut down time
	- detect cloud latency issues
	- optimize cloud resource utilization
	- optimize modern cloud architectures
- User experience
##### <span style="color: #d79921">Pillars of observability</span>
##### <span style="color: #d79921">Cloud native observability</span>
##### <span style="color: #d79921">Sampling</span>
##### <span style="color: #d79921">IBM Instana Obervability</span>
##### <span style="color: #d79921">Telemetry</span>
---
Process of collecting and transmitting data from remote or inaccessible sources to be monitored and analyzed.

It's often used in fields such as aviation, medicine,  and environmental monitoring to gather information about  a system's performance or conditions without direct human interaction.

In technology, telemetry can  refer to collecting of data from devices  such as smartphones or  interconnected appliances for  analysis and optimization purposes.

Telemetry enables to: collect and analyze data, provide valuable information

- <strong style="color: white">Benefits:</strong>
	- provides remote feedback without requiring user interaction
	- allows for real-time monitoring of application performance
	- allows tracking of user activity and experience (engagement frequency,  device configurations, and crashes)
	- helps with network analytics and security --> prevent breaches

Types of telemetry
- Performance telemetry --> how the application is performing
	- response time, throughput, and resource utilization
- Usage telemetry --> how users interact with the application
	- features are being used most frequently,  and which ones are ignored
- Error telemetry --> errors that occur within the application
	- stack traces and error messages
- Security telemetry --> information about security events
	- failed login attempts or unauthorized access attempts
	- can be used to identify potential security threats and implement appropriate measures to mitigate them

How it works - components
Sensors --> Transmitters --> Receivers
Sensors: measure physical quantities, can be either analog or digital
Transmitters: convert the signal into a required format, sen information to a collection point (Ex: satellite or base station)
Receivers: captura the signal at the destination, forward it on to processing systems, extract useful information from raw data using algorithms

Steps to implement

Define the telemetry goals --> Choose the right data collection tools --> Desgin the teletry shcema --> Implement telemetry collection --> Analyze the collected data --> Iterate on the design 

teletry shcema --> defines what data you will collect and how it will be structured. Consider factors like data types, naming conventions,  and aggregation levels when defining your schema.

Telemetry and distributed tracing are  interrelated concepts used in software engineering, specifically in developing distributed systems.
Distributed tracing is a technique of observing requests transmitted for  distributed Cloud environments
- traces the path of a request through several node and services in real time

Telemetry tools: Datadog, Dynatrace, New Relic, Sumo Logic, Instana
Distributed tracing tools: Atatus, Jaeger, Zipkin, Dynatrace

Tracing for container-based applications  involves capturing and analyzing the flow of the requests between different application components. Tracing assumes even greater significance because of the distributed nature of the microservices architecture in a containerized environment.

implement tracing

Choose a tracnign tool - intrument the code - configure the tracing agent - deploy the tracer - verify functionality

Distributed tracing tracks the flow of application requests from front-end component or devices to back-end services, databases, and other third-party services.

Best pratcies: instrument services with code, implement end-to-end intrumentation adn recird traces, pay attention to duration metrics, follow OpenTelemetry, OpenTracing and OpenCensus standardization