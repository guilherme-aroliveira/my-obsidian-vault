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
###### <span style="color:#689d6a">Organization impact of DevOps</span>

Part of becoming a DevOps organization is to first become <span style="color: #d65d0e">Agile</span>, because <strong style="color: #b16286">Agile is a fundamental tenet of DevOps</strong>. 

>[!info]
>Agile teams must be small, dedicated teams, cross-functional teams, self-organizing teams

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
###### <span style="color:#689d6a">Site Reliability Engineering</span>

<span style="color: #d65d0e">Site Reliability Engineering</span> <span style="color: #3588E9">--></span> "Is what happens when a software engineer is tasked with what is used to be called operations."

<strong style="color: #d79921">Tenets of SRE</strong><ul><li>Hire only software engineers</li><li>Site reability engineers work on reducing toil through automation</li><li>SRE teams are separated from development teams</li><li>Stability is controlled through error budges</li><li>Developers rotate through operations</li></ul>
DevOps maintains stability by using automation through Continuous Delivery pipelines, and by making sure that everyone is responsible for the code that runs in production.

Both seek to make development and operations visible to each other. Both requires a blameless culture. The objective of both is to deploy software faster with stability.

<span style="color: #3588E9">--></span> SRE and DevOps can be use together to both maintain and use computer infrastructure.
###### <span style="color:#689d6a">Security by Design</span>

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
## **Unix**
---
Whenever a Linux system builds up, it starts with just one process with a process ID of one. This is the root process and kicks off all the other processes in the system. By the time the system boots up completely, we have a handful of processes running. This can be seen by running the PS command to list all the running processes.

IDs are unique and two processes cannot have the same process ID.

The text based command line interface that helps you run commands to interact with the operating system is called the Linux shell

there are different kinds of shells such as The Bourne Shell, the C Shell, Z Shell, born again Shell, which is known as Bash. And each of these shells behave differently

Every Linux system has a super user known as the root user. The root user has no restrictions on the system and can perform any task, which is why in most production environments or enterprise environments, access to the root user is restricted and you will almost never log in to the systems as a root user. To edit sudo rules --> /etc/sudoers

Kernel

Linux Kernel is a program that needs to be loaded into memory and run. That operation is done by a boot loader, like GRUB. 

GRUB reads the kernel file from disk into memory and transfers controls to it.

The kernel has command-line parameters. And GRUB is responsible for passing those parameters to the kernel. The Kernel also have an API.

The functions that are called from user space into the kernel are called system calls. But the Linux Kernel also provides virtual file systems: proc, sys and debugfs. Through those virtual file systems  is possible to interact directly with kernel, getting information from it and changing things in the kernel.

The file system also has devices files which receive interactions by doing operations on those devices files. Those are standard system calls like read, write and open. 

The kernel enforces privileges, which in Linux are called capabilities. In the Linux kernel source code, it refers to the capabilities of a process to see if it is allowed to perform some sort of privileged information. Ex: root processes have all the privileges.

The Linux kernel also implements a number of security policies. Ex: the underlying mechanisms used by SE Linux.
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
<span style="color: #d65d0e">Source code management</span> (or SCM) is the <strong style="color: #b16286">practice of tracking versions of source code</strong> as it is developed. SCM tolls are also referred to as version control systems (VCS)

SCM can be centralized or distributed. A centralized SCM stores code repository and version history centrally. With distributed SCM, each developer has a local clone of code repository and version history.

[[Git]]  <span style="color: #3588E9">--></span> is a <strong style="color: #b16286">software that keeps track of changes</strong> that are made of files and directories. It allows to move back and forth between the versions
- Is referred to as a version control system (VCS). The <strong style="color: #b16286">primary purpose is to manage</strong> source code <span style="color: #3588E9">--></span> source code management (SCM)
- Git is the current standard for version control software.

Remote platforms (repository managers) alto referred as <strong style="color: #d79921">central repository</strong>, make it easier for team work with Git. They <strong style="color: #b16286">provide additional capabilities</strong> that surround Git repositories. It's normally hosted on a remote server or located within a Gt repository management service.

<span style="color: #d65d0e">Remote Server</span> <span style="color: #3588E9">--></span> simply install Git into the hosting environment and set a up anew repository with the command: `git init --bare` This option is chosen if it's not required a more full-feature Git hosting solution, it's unable to host code on a third-party service.

<span style="color: #d65d0e">Repository Manager</span> <span style="color: #3588E9">--></span> cloud-based service or on-premises installation. includes capabilities such as: issue tracking, pull requests, code review, access controls, inline editing.

Some of the most popular repository hosts are:
- <span style="color: #689d6a">GitHub</span> <span style="color: #3588E9">--></span> cloud hosting, open-source leader, REST API to access data, Gists feature for sharing small code snippets.
- <span style="color: #689d6a">GitLab</span> <span style="color: #3588E9">--></span> cloud and self-hosting (completely free), CI capabilities support via its GitLab Runner feature, Cycle analytics.
- <span style="color: #689d6a">Bitbucket</span> <span style="color: #3588E9">--></span> multi-platform, Jira integration, Confluence integration. 
##### <span style="color: #d79921">Distributed VCS</span>

Different users maintain their own repositories, instead of working from a central repository.

Changes are stored as sets or patches, and <strong style="color: #b16286">it's focused on tracking changes</strong>, not version of the documents. Git really focus on these changes sets and encapsulating a change set as a discrete unit, and then those changes sets can be changes between repositores.

There is no single master repository, there's just many working copies, each with their own combination of changes sets.

<strong style="color: white">By convention</strong> users often do designate a repository as beings the master repository, but that <strong style="color: #b16286">it's not a part of the Git architecture</strong>, it's just a convention.

The users can actually have three or four different master repositories that have different versions in them.

There's no need to communicate with a central server. it's not necessary to have network access to submit the changes. And there's no single point of failure.
##### <span style="color: #689d6a">Git</span>

Git stores configuration information in three places: system, user and projects. At the <strong style="color: #d79921">system level</strong>, git stores configuration in the directory: `/etc/gitconfig`

At the <strong style="color: #d79921">user level</strong> , the configuration is located on the `gitconfig` file on the `home` directory <span style="color: #3588E9">--></span> `/.gitconfig` or `$HOME/.gitconfig`

>[!info]
>A configuração ao nível do sistema é a primeira e mais abrangente. É uma configuração aplicada a todo usuário do sistema por padrão.

At the <strong style="color: #d79921">project level</strong> the configuration is located at: `project/.git/config`

>[!note]
>The directory `.git` is all of Git tracking, if it's deleted, git would be removed from the project, this directory is the tracking. Git <strong style="color: white">centralizes everything</strong> into `.git`

The `git config` command allows to edit configurations in all three levels, following a modifier that indicates each level will be: 
- <code style="color: #689d6a">$ git config --system</code>

O comando `git help` exibe a documentação de qualquer comando informado: `git helpo log`. Há também o comando `main` que irá exibir o manual do comando informado: `man git-log`.

<strong style="color: #c6554f">Git workflow</strong>
- workspace <span style="color: #3588E9">---></span> ( `git add` )  <span style="color: #3588E9">---></span> staging <span style="color: #3588E9">---></span> ( `git commit` ) <span style="color: #3588E9">---></span> local repository <span style="color: #3588E9">---></span> ( `git push` ) <span style="color: #3588E9">---></span> remote repository

<strong style="color: #c6554f">Git repository guidelines</strong>
- create a separate Git repository for each component
- create a new branch for every issue
- use pull request do merge to master
- every pull request is an opportunity for a code review

<strong style="color: #c6554f">Pull request workflow</strong>
- GitHub (remote main) <span style="color: #3588E9">---></span> Git (local main) <span style="color: #3588E9">---></span> local branch <span style="color: #3588E9">---></span> remote branch <span style="color: #3588E9">---></span> remote main
- <code style="color: #689d6a">$ git checkout main</code> <span style="color: #3588E9">--></span> <code style="color: #689d6a">$ git pull main</code> <span style="color: #3588E9">--></span> <code style="color: #689d6a">$ git git checkout [branch]</code> <span style="color: #3588E9">--></span>  <code style="color: #689d6a">$ git merge main</code> <span style="color: #3588E9">--></span>  <code style="color: #689d6a">$ git push -u origin [branch]</code>
##### <span style="color: #d79921">Git for Teams</span>

<span style="color: #d65d0e">Golden rule of Git</span> <span style="color: #3588E9">--></span> commit early and commit often 

Keep the commit small in scope and focus single feature per commit. Small-scoped commit are much easier to share with team members. Small and frequent commits are very beneficial.

Keep branch names, short, consistent and informative. Example: `bug/123/menu-issue` <span style="color: #3588E9">--></span> type of change/change number, short name

Establish a naming conventions

>[!note]
>Only test new commands on the local repository and on a safe branch.
###### <span style="color:#c6554f">Commit messages</span> 

Use a text editor to write a great commit message instead of the command line:

- `git config --global core.editor /usr/bin/kate`

Set up a standard message template <span style="color: #3588E9">--></span> to draft commit messages that are uniform and more robust. Start with a subject line, describe the commit and what it was created, specifies the work items:

- `git config commit.template "/home/Desktop/repos/.gitmessage.txt"`

Auto setting is useful when working in a cross-platform environment:
- convert carrot to line field <span style="color: #3588E9">--></span> `git config core.autocrlf input`
- `input` <span style="color: #3588E9">--></span> commit carriage return line feed to line feed when a commit is made
###### <span style="color:#c6554f">Teams</span>

The approach to Git will need to be adjusted according to the size and composition of the team.

For <strong style="color: white">teams of 1 or 2</strong> (Small Team) <span style="color: #3588E9">--></span>  all members act as a maintainer

For <strong style="color: white">middle teams</strong> (normal size) <span style="color: #3588E9">--></span> 3 integrators or maintainers that will merge contribution from contributors. These individuals are often the most senior members of the team and are responsible for performing a review of the contributing code prior to its merging.

For <strong style="color: white">large teams</strong> <span style="color: #3588E9">--></span> such as  massive open-source projects, for the large community of contributors, there will be many integrators with common permissions.

<span style="color: #d65d0e">Dictator Model</span> <span style="color: #3588E9">--></span> act as a second-level approving authority  merging contributions from the integrators for lieutenant repositories. This model manages the Linux Project.
###### <span style="color:#c6554f">Workflows</span>

<span style="color: #d65d0e">Trunk-base development</span> (TBD) <span style="color: #3588E9">--></span> updates ad pulls occur from a single branch named trunk. 
- it reduces the problems tat frequently occur when merging long-lived branches, such as breaking the build, duplicate work, and incompatible changes.
- it can involve cherry-pick --> allows a commit in one branch to be applied to another, is often used to pull a hotfix into a release branch from trunk

>[!note]
>Obs: branching from trunk such as when using a feature branch, is not acceptable.

<strong style="color: white">TBD Best practices:</strong>
- small commit on a daily basis
- organize work into small tasks
- tightly integrated with Ci/Cd practices 
- release ready
 
<span style="color: #d65d0e">Gitflow</span> <span style="color: #3588E9">--></span> popular workflow for Git that centers around two long-lived branches: master and develop. 
- the master branch contains a copy of the current production code and is tightly controlled. Develop is the parent branch for feature branches that are crated to address a particular line of work.
- once a feature is complete is merged into develop branch.
- a release branch is created to release new features.
- in a release branch, bug fixes can be made prior to the release in parallel to new work being performed in develop.
- release branch is merged into master and develop branches.
- feature branches contain new releases, and they need to merge into the develop branch before the master.

>[!note]
>Gitflow involves code review of the changes that have been requested to be merged practing branches and issues.

<strong style="color: white">Gitflow Benefits:</strong>
- the workflow is based around release
- allows for parallel development by leveraging short-lived branches for features, hotfixes, and releases.
- pull/merge requests used for updates to master and develop
## **Virtualization**
---
##### <span style="color:#689d6a">Virtual Machines</span>

A virtualização permite criar diversas aplicações e servidores sem a necessidade de coexistirem. Porém, os recursos dd máquina host (physical host) serão divididos. Cada vm (virtual machine) pode estar em sistemas operacionais distintos. 

The <strong style="color: white">objective</strong> of the virtualization is to <strong style="color: #d79921">chop the server up into smaller chunks</strong>, so that each one of these chunks can potentially contain an application. The vm stays on top of the hypervisor. 

<span style="color: #d65d0e">hypervisor</span> <span style="color: #3588E9">--></span> a software that can virtualize the hardware resources. It's the hypervisor job to manage the resources for every virtua system. It creates multiple machines, and each machine can run its own guest OS.

>[!info]
>The guest OS doesn't know that is talking to the hypervisor

<span style="color: #d65d0e">vm image</span> <span style="color: #3588E9">--></span> machine level isolation

The <strong style="color: #b16286">hypervisor is what controls and allocates what portion of hardware resources each operating system should get</strong>, in order every one of them to get what they need and not to disrupt each other.

The hypervisor splits the physical hardware into the number of VMs that can be chosen. Virtual Machines allow users to grow up control in terms of what exactly the kind of environment. 

<strong style="color: white">Virtualization - drawbacks:</strong>
- <span style="color: #98971a">amplified physical failures</span> <span style="color: #3588E9">--></span> if the machine goes down, all of the VMs goes down together
- <span style="color: #98971a">performance reduces</span> <span style="color: #3588E9">--></span> some applications do not work well in a virtualized environment

To check if virtualization is supported on Linux:  
- <code style="color: #689d6a">$ grep -E --color 'vmx|svm' /proc/cpuinfo</code>

<span style="color: #98971a">Vagrant</span> <span style="color: #3588E9">--></span> created by Hashicorp, is a tool for creating and managing virtual machines, on different platforms and operating systems.
##### <span style="color:#689d6a">Containers</span>

An <span style="color: #d65d0e">image</span> <strong style="color: #b16286">is a package or a template</strong>, just like a VM template that you might have worked with in the virtualization world. <strong style="color: #b16286">It is used to create one or more containers.</strong>

<span style="color: #d65d0e">Containers</span> <strong style="color: #b16286">are running instances of images</strong> that are isolated and have their own environments and set of processes. It's a way of packaging all of the configuration and dependencies to run a program into a small bundle of code that can be run on any machine or operating system.

>[!info]
>The container image doesn't have the OS Kernel, it has a slim version of all OS utilities that's needed to run the container.

A <span style="color: #d65d0e">container</span>, powered by the <span style="color: #d65d0e">containerization engine</span>, is a <strong style="color: #d79921">standard unit of software</strong> that encapsulates everything (applications code, runtime, system tools, system libraries) that programmers need to build, ship and run applications efficiently.

A container is an isolated process that consist of the following items, all bundled into one package:
- the application code
- thee required dependencies (e.g. libraries, utilities, configuration files)
- the necessary runtime environment to run the application

>[!info]
>Containers solve the problem of making software portable so that applications can run on multiple platforms. This is possible because <strong>containers are platform-independent</strong> and can run on the cloud, desktop, and on-premises, and <strong>they are operating system-independent</strong>, which means they can run on Windows, Linux or Mac Os.

The container engine virtualizes the operating system and are responsible for running containers.

Unlike virtual machines, containers are not meant to host an operating system. Containers are meant to run a specific task or process, such as to host an instance of a web server or application server or a database.

The container gives the ability to run more applications and more workloads on the infrastructure. The notion of containers is to take care of all drawbacks that has been hampering the applications landscape.

<strong style="color: #d79921">Container technology</strong> is a <strong style="color: #b16286">method of packaging an application so it can run with isolation dependencies</strong>. Containers allows to package the application in a way which contains not just the application code, but also the dependencies including the environment. 

>[!note]
>A container only leaves as long as the process inside it is alive. If the web service inside the container is stopped or crashed, then the container exits

Container allow to bundle the application in a way that is depoyable on any environment, on any machine, on any cloud provider. it gives the ability to move the application from one environment to the other, but it also gives very high portability. 

<strong style="color: white">Benefits of containers:</strong>
- containers make easier for developers to create, deploy, and run applications on different hardware and platforms, quickly and easily
- containers share an single kernel and share application
- containers cause a lower system overhead as compared to virtual machines

There are many popular container vendors today, which include: [[Docker]], <span style="color:#98971a">Podman</span>, <span style="color:#98971a">LXC</span> and <span style="color:#98971a">Vagrant</span>.
- <span style="color:#98971a">Docker</span> <span style="color: #3588E9">--></span> the most popular container platform today.
- <span style="color:#98971a">Podman</span> <span style="color: #3588E9">--></span> daemon-less container engine that is more secure than Docker.
- <span style="color:#98971a">LXC</span> <span style="color: #3588E9">--></span> preferred for data-intensive apps and operations.
- <span style="color:#98971a">Vagrant</span> <span style="color: #3588E9">--></span> offers the highest levels of isolation on the running physical machine.

<span style="color:#98971a">busybox</span> <span style="color: #3588E9">--></span> it's a binary that contains many well know Unix tools like <span style="color: #98971a">awk</span>, <span style="color: #98971a">date</span>, <span style="color: #98971a">whoami</span>, <span style="color: #98971a">wget</span>.

Container based virtualization is the option being adopt by most PaaS cloud players. <strong style="color: #d79921">Containers are all process based</strong>, so they have less isolation than a VM. Containers usually take mili-seconds to start, while a VM may take minutes. 
###### <span style="color:#98971a">Amazon ECR</span>

<span style="color: #d65d0e">Elastic Container Registry (ECR)</span> is a <strong style="color: #b16286">fully-manage Docker container registry</strong> by AWS.

The repository URI is what uniquely identifies the repository and the images that are being checked on it. When it starts creating clusters, the access to the particular image is needed, which tells where it's stored.  

<span style="color: #d65d0e">push commands</span> <span style="color: #3588E9">--></span> return all the commands used to push the images on ECR
- `aws ecr get--login --region us-east-1`
- `docker build -t helloworld`
- `docker tag helloworld:latest <ecr>`
- `docker push <ecr>`
## **Container Orchestration**
---
<span style="color: #d65d0e">Container orchestration</span> is a process that automates the container life cycle of containerized applications, which includes: Deployment, Management, Scaling, Networking and Availability. It can be implemented on-premises, an on public, private, or multi-cloud environments. Container orchestration solves the problem of deploying multiple containers across many hosts.

<span style="color: #d65d0e">Container orchestration</span> <strong style="color: white">features</strong><strong style="color:#3588E9"> :</strong> defines container images and registry, improves provisioning and deployment, secures network connectivity, ensures availability and performance, manages scalability and load balancing, resource allocation and scheduling, rolling updates and roll backs, health checks and automated error handling.

<span style="color: #d65d0e">Container orchestration</span> <strong>uses configuration files</strong> written in <span style="color:#98971a">YAML</span> or <span style="color:#98971a">JSON</span>. These files configure each container so it can find resources, establish a network, and store logs. Container orchestration manages the container's life-cycle based on specifications in the configuration file. This includes system parameters (like CPU and memory), and file parameters (like proximity and file metadata). And container orchestration supports scaling and enhances productivity, through automation.

Some of the well-know <strong style="color: #d79921">container orchestration tools</strong> are: <span style="color:#98971a">Marathon</span>, <span style="color:#98971a">Hashicorp's Nomad</span>, AWS ECS, [[ Docker Swarm ]] and [[ Kubernetes ]]
- <span style="color:#98971a">Marathon</span> <span style="color: #3588E9">--></span> is a framework for Apache Mesos, and open-source cluster manager that was developed by the University of California at Berkeley. It allows the developer to scale container infrastructure by automating the bulk of management and monitoring tasks.
- <span style="color:#98971a">Hashicorp's Nomad</span> <span style="color: #3588E9">--></span> is a free and open-source cluster management and scheduling tool that supports Docker and other standalone, virtualized, or containerized applications on all major operating systems across all infrastructure, whether on-premises or in the cloud.
- <span style="color:#98971a">Docker Swarm</span> <span style="color: #3588E9">--></span> it's the cluster management and orchestration feature that was designed specifically to work with Docker Engine and other Docker tools. It's functionality comes from a separate project that Docker calls Swarmkit.
- <span style="color:#98971a">Kubernetes</span> <span style="color: #3588E9">--></span> it's an open-source platform developed by Google, and it's the de facto standard for container orchestration. Kubernetes automates a host of container management tasks like: deployment, storage provisioning, load balancing and scaling, service discovery and "self-healing".

>[!info]
>Container orchestration helps to meet business goals and increase profitability by using <span style="color: #d65d0e">automation</span>.
###### <span style="color: #d79921">Elastic Container Service (ECS)</span>

<span style="color: #d65d0e">ECS</span> is an <strong style="color: #b16286">orchestration service that supports Docker</strong>, used for automating deployment, scaling and managing the containerized applications. 

Some of the <strong style="color: white">features</strong> include:
- launching and stooping Docker containers
- scaling the application
- query the state of the applications
- schedule long-running applications

<span style="color: #d65d0e">Docker</span> is <strong style="color: #d79921">the only container-runtime platform supported by Amazon ECS</strong>. Other container-runtime tools available in the industry are Rocket, LXD, OpenVZ and more.

ECS receives the docker image and maintain the entire cluster, including scaling principles (like Kubernetes environment, but in a form of managed service by AWS).

<span style="color: #d65d0e">Fargate</span> <span style="color: #3588E9">--></span> it'a an <strong style="color: #b16286">AWS managed service</strong> (serverless infrastructure) that allows to set all the configuration in a UI.
- underlying EC2 instances don't have to be managed
- run containers without having to manage infrastructure
- total integration and part of AW Elastic Container Service (ECS)
- it uses an on-demand pricing model

<strong style="color: white">Best practices:</strong>
- One EC2 instance to one TASK
- One task to one Container

One task to many containers <span style="color: #3588E9">--></span> not recommended by AWS

<strong style="color: #b16286">An amazon ecs clusters is a logical grouping of tasks or services</strong>. The tasks and services run on infrastructure that is registered to a cluster.  The infrastructure capacity can be provided by AWS Fargate.

<strong style="color:#98971a">Task definitions</strong>
- task are a <strong style="color: #b16286">group of containers</strong> that live and terminate together
- memory limit <span style="color: #3588E9">--></span> softy (default) and hard limit

>[!info]
>The number of tasks basically determines at what rate the application is getting the data on request from the customers.
## **Cloud Computing**
---
It is a <strong style="color: #b16286">business model that allows the use of on-demand computing resources through network connections</strong>. In addition, Cloud computing enables efficient marketing of applications regardless of maintenance and cost.

<span style="color: #d65d0e">NIST</span> <span style="color: #3588E9">--></span> National Institute of Standards and Technology

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

<span style="color: #d65d0e">Infrasctructure as a Service (IaaS)</span> is a set of compute, networking and storage resources that have been virtualized by a vendor so that a user can access and configure them. In the IaaS model, the cloud provider manages the physical resources: data centers, cooling, power, networking & security, servers & storage

<span style="color: #d65d0e">Platform as a service (PaaS)</span> takes advantage of all the virtualized resources from IaaS and then just abstracts them away, so the user doesn't have to worry about managing any of those virtualized resources. The provider manages the platform infrastructure: operating system, development tools, databases.

<span style="color: #d65d0e">Software as a Service (SaaS)</span> is just software that the user don't have to install on his machine and he doesn't have to manually update. The cloud provider hosts and manages applications and data. The user for SaaS could be anyone. Example os SaaS: Gmail.

The <strong style="color: #b16286">Pyramid Metaphor</strong>, is meant to indicate that as we move down, we increasing complexity in terms of knowledge and management of infrastructure resources and we're increasing the ease of use.

<strong style="color: #b16286">Car Metaphor:</strong>
- IaaS = leasing
- PaaS = renting
- SaaS = taxi
##### **<span style="color:#689d6a">Deployment Models</span>**

Deployment models indicate where the infrastructure resides, who owns and manages it, and how cloud resources and services are made available to users. The four cloud deployment models include: Public Cloud, Private Cloud, Community Cloud and Hybrid Cloud.
###### <span style="color: #d79921">Public Cloud</span>

A public cloud is a <strong style="color: #b16286">virtualized multi-tenant architecture</strong> enabling tenants or users to share computing resources (shared environment by a third-party provider).

Users can access servers, storage, network, security and applications as services delivered on-demand by cloud service providers over the internet. Using web consoles and APIs, users can provision the resources and services they need.

The cloud provider owns, manages, provisions and maintains the infrastructure. The user pays for what he use within a certain period.

Public clouds offer significant cost savings in terms of Total Cost for Ownership (TCO) as the provider bears all the capital, operational, and maintenance expenses for the infrastructure and the facilities they are hosted in.

<strong style="color: white">Characteristics:</strong>
- Resources are distributed on an as-needed basis offered through a variety of subscription and pay-as-you-go models.
- Lower cost, less maintenance.
###### <span style="color: #d79921">Private Cloud</span>

Used exclusively by a business/organization. Services are delivered over a private network.

Hosted by on-prem datacenters or dedicated hardware hosted by a third party providers - involves CAPEX (Capital Expenditure)

More control, higher flexibility, higher maintenance 
###### <span style="color: #d79921">Hybrid Cloud</span>

<strong style="color: #b16286">Cloud infrastructure provisioned for exclusive use</strong> by a single organization comprising multiple consumers, such as the business units within the organization. It may be owned, managed, and operated by the organization, a third party or some combination of them, and it may exist on or off premises.

Private cloud platforms can be implemented internally or externally.

When it is provisioned over a cloud providers infrastructure, it is owned, managed, and operated by the service provider. This external private cloud offering that resides on a cloud service providers infrastructure is called a <span style="color: #d65d0e">Virtual Private Cloud</span> or VPC.

>[!info]
>A <span style="color: #d65d0e">VPC</span> is a public cloud offering that lets an organization establish its own private and secure cloud-like computing environment in a logically isolated part of a shared public cloud.

A private cloud is a virtualized environment modeled to bring in the benefits of a public cloud platform without the perceived disadvantages of an open-end shared public platform.

>[!note]
>Using a VPC, organizations can leverage the dynamic scalability, high availability, and lower cost of ownership of a public cloud, while having the infrastructure and security tailored to the organization's unique needs.

<span style="color: #d65d0e">cloud bursting</span> <span style="color: #3588E9">--></span> leveraging public cloud instances for a period of time, but returning to the private cloud when the surge is meet.

- <strong style="color: white">Benefits:</strong>
	- Controlled by internal IT
		- <strong style="color: white">Use Cases:</strong>
			- modernizing in-house & legacy applications
			- build applications anywhere and move them without compromising security or compliance
			- full control over critical security and compliance issues within dedicated cloud
	- Reduced Costs
	- Better scalability --> through virtualization and cloud bursting
	- Controlled access & security
	- Greater agility
###### <span style="color: #d79921">Community Cloud</span>

“<strong style="color: #b16286">Cloud infrastructure that is provisioned for exclusive use by a specific community of consumers</strong> from organizations that have shared concerns (e.g., mission, security requirements, policy, and compliance considerations). It may be owned, managed, and operated by one or more of the organizations in the community, a third party, or some combination of them, and it may exist on or off premises.” (NIST definition)
##### **<span style="color:#689d6a">Cloud Infrastructure</span>**

The <strong style="color: #b16286">infrastructure layer is the foundation of the cloud</strong>. This layer consists of physical resources that are housed in Regions, Zones and Data Centers.

A <span style="color: #d65d0e">cloud Region</span>, is a <strong style="color: #b16286">geographic area or location where a Cloud provider’s infrastructure is clustered</strong>, and may have names like NA South or US East. The cloud Regions are isolated from each other so that if one Region was impacted by a natural disaster like an Earthquake, the Cloud operations in other Regions would keep running.

Each Cloud Region can have multiple Zones (or Availability Zones or AZ for short), which are typically distinct Data Centers with their own power, cooling and networking resources. These Zones can have names like DAL-09 or us-east-1. <strong style="color: #d79921">The isolation of zones improves the cloud’s overall</strong> fault tolerance, decreases latency, and avoids creating a single shared point of failure.

>[!info]
>A cloud Data center is a huge room or a warehouse containing cloud infrastructure.

Cloud providers offer several compute options – Virtual Servers, Bare Metal Servers, and “Serverless” computing resources. <strong style="color: #d79921">Most of the servers in a cloud Data Center run hypervisors</strong> to create virtual servers or virtual machines (also called VMs for short), that are software-based computers, based on virtualization technologies.

<span style="color: #d65d0e">Virtual Machines</span> or VMs are also known as Virtual Servers or Virtual Instances, or simply instances, depending on the cloud provider. When  a virtual server is created on the cloud, the Region and Zone or Data Center are specified that the server to be provisioned in and the Operating System to be used.

>[!info] 
>shared (that is, a multi-tenant) VMs or dedicated (that is, a single-tenant) VMs.
##### **<span style="color:#689d6a">Cloud Storage</span>**
## **Infrastructure as Code**
---
<span style="color: #d65d0e">Infrastructure as Code (IaC)</span> <span style="color: #3588E9">--></span> is the practice of describing infrastructure in textual format that is executable. The tools to configure infrastructure are called <span style="color: #d65d0e">Configuration Management Systems</span>, like <span style="color:#98971a">Ansible</span>, <span style="color:#98971a">Puppet</span> or <span style="color:#98971a">Chef</span>, that allows to describe the infrastructure as code and then creating that infrastructure and keep it in that way.

<span style="color: #3588E9">--></span> <strong style="color: #b16286">Server drift</strong> is a major source of failure. "Server are cattle not pets". Infrastructure is transient.

<span style="color: #d65d0e">Configuration Management Systems (CMS)</span> predated the IaC tools.

IaC tools can be either <strong>declarative</strong> or <strong>imperative</strong>. In a <strong style="color: #b16286">declarative approach</strong>, the desired state of the infrastructure resources to be provision. Tools that use this approach: [[ Terraform ]], <span style="color:#98971a">Puppet</span>, <span style="color:#98971a">SaltStack</span>, [[CloudFormation]] and [[ Ansible ]]. The <strong style="color: #b16286">imperative approach</strong>, requires to define the specific order of commands needed to achieve the sired state. The tools executes commands in that order. Tools that use imperative approach: <span style="color:#98971a">Chef</span> and <span style="color:#98971a">Ansible</span>.

IaC can be broadly classified into three types: Configuration Management, Server Templating and Provisioning Tools.

<span style="color: #d65d0e">Configuration Management</span> <span style="color: #3588E9">--></span> managing and operating system configuration including installed packages, device configurations, users, groups, etc. Tools like Ansible, Chef, Puppet and Salt Stack fall into this category, which are commonly used to install and manage software on existing infrastructure resources such as servers, databases, networking devices, etc...

>[!info]
>Configuration management tools maintain a consistent and standard structure of code, and this makes it easier to manage and update it as needed. They're also designed to run on multiple remote resources at once.

<span style="color: #d65d0e">Proviosing</span> <span style="color: #3588E9">--></span> getting and setting the physical components to run specific applications. Tools like Terraform and CloudFormation are used to provision infrastructure components using a simple declarative code.

<span style="color: #d65d0e">Server Templating Tools</span> <span style="color: #3588E9">--></span> these are tools like Docker, Vagrant and Packer from Hashicorp that can be used to create a custom image of a virtual machine or a container. These images already contain all the required software and dependencies installed on them.

<strong style="color: white">Benefits</strong> of <span style="color: #d65d0e">IaC</span>: faster time to production, more efficient development, protection against staff churn, lower costs and improved use of developer time, and idempotente.

<span style="color: #d65d0e">In place update</span> <span style="color: #3588E9">--></span> use the same software upgrade life cycle for each server using the same approach

>[!info ]
>The underlying infrastructure remains the same, but the software and the configuration on each server are changed as part of the update <span style="color: #3588E9">--></span> <strong style="color: #d79921">Multable Infrastructure</strong>

<span style="color: #d65d0e">Configuration drift</span> <span style="color: #3588E9">--></span> when servers vary from one another, which can be in software configuration or operating system, etc.

Immutable infrastructure --> 

> [!note]
> With infrastructure as a code, immutability makes it easier to version the infrastructure and to roll back and roll forward between versions.
## **Serverless Architecture**
---
Serverless is an  <strong style="color: #b16286">approach to computing that offloads responsibility for common infrastructure management tasks</strong> such as scaling, scheduling, patching, and provisioning application stacks to cloud providers

Serverless doesn't mean there are no servers, only that the management of the underlying physical or virtual servers is removed from their users

The serverless computing environment allocates resources as needed for the applications.

<strong style="color: white">Attributes:</strong>
- no provisions of servers
- runs code only-on demand
- pay only for resources being used

>[!info]
>Effectively, serverless abstracts the infrastructure away from developers, code is executed as individual functions, where each function runs inside a stateless container.

Some of the key serverless computing services today include: IBM Cloud functions, which is based on Apache Open Whisk, AWS Lambda and Microsoft Azure functions.

Applications that qualify for a <strong style="color: #d79921">serverless architecture</strong> include some of the following characteristics: short-running stateless functions, seconds or minutes, seasonal workloads with varying off peak and peaks, production volumetric data that shows too much idle time, event-based processing or asynchronous request processing for implementing use cases.

<strong style="color: white">Use Cases:</strong>
- data and event processing
- IoT
- Micros services
- Mobile backends

Serverless is well suited to working with structured text, audio, image, and video data around tasks such as data enrichment, transformation, validation, and cleansing, DF processing, audio normalization, thumbnail generation, and video transcoding.

>[!info]
>For workloads characterized by long-running processes, managing a traditional server environment might be simpler and more cost effective.
##### **<span style="color:#689d6a">Serverless Computing</span>**

<span style="color: #d65d0e">serverless</span> <span style="color: #3588E9">--></span> "The concept of building and running applications that do not require server management" (CNCF).

Serverless computing offloads the responsibility of infrastructure management to cloud providers, enabling developers to focus on the application business logic.

<strong style="color: white">Best practices</strong>:
- Make each function perform only one action
- Avoid function chaining
- Limit dependencies on third-party libraries

<strong style="color: white">Charasterictics</strong>: Host-less, Elastic, Load balanced, Stateless, Event driven, Highly available, Usage-based/granular billing

<strong style="color: #d65d0e">FaaS Model</strong>
- Function as a Service (FaaS) --> cloud computing service that allows to execute code in response to events without complex infrastructure.
- <strong style="color: white">Charasterictics</strong>: 
	- Creates applications as functions; 
	- Deploys on hybrid and on-premise; 
	- Stateless; 
	- Includes functions that execute in milliseconds and are instantaneously scalable; 
	- Lightweight and decoupled; 
	- Billed on consumption and execution.
- <strong style="color: white">Benefits</strong>: 
	- divides server into functions, 
	- pay for what you use, 
	- inherent high availability.

<strong style="color: white">Self-managed FaaS</strong>:AWS Lambda, Google Cloud Functions, Azure Functions, IBM Cloud Functions, Openshift Cloud Functions(Red Hat).

<strong style="color: white">Managed FaaS providers</strong>:
- <span style="color: #98971a">Fission</span> <span style="color: #3588E9">--></span> framework for serverless function on Kubernetes
- <span style="color: #98971a">Fn Project</span> <span style="color: #3588E9">--></span> a container-native serverless platform
- <span style="color: #98971a">Knative</span> <span style="color: #3588E9">--></span> Kubernetes-based platform to build, deploy, and manage serverless workload
- <span style="color: #98971a">OpenFass</span> <span style="color: #3588E9">--></span> allows to turn any Linux or Windows process into a function

<strong style="color: #d79921">Architecture concepts</strong>
- Abstracts infrastructure and software environment.
- Code runs in a cloud platform.
- Cloud provider manages the hardware and software setup, security, performance.
- Billed only for usage
- Developers only need to focus on applications and code in the form of functions.
###### <span style="color: #d79921">Constrains</span>

- Unsuitable for long-running processes
- Vendor lock-in risks
- Cods starts
- Latency unsuitable for time-critical apps
- Security concerns
- Complex monitoring and debugging
- Language support dependency
- Server optimization loss
- No state persistence
###### <span style="color: #d79921">Stack components</span>

FaaS, BaaS and API gateway.

<span style="color: #98971a">Events</span> <span style="color: #3588E9">---></span> <span style="color: #98971a">API Gateway</span> <span style="color: #3588E9">---</span> { requests } <span style="color: #3588E9">---></span> <span style="color: #98971a">Functions</span> <span style="color: #3588E9">---></span> <span style="color: #98971a">BaaS</span> (File storage, Block Storage)

Events request can be <span style="color: #d65d0e">webhooks</span> from repositories such as GitHub and Docker Hub, and scheduled jobs. 

The functions then process these requests, and they are further directed (if necessary) toward the backend services. 

The output or response is then sent back to the client through the FaaS component and the API Gateway.
###### <span style="color: #d79921">The Serverless Framework</span>

The <span style="color: #d65d0e">Serverless Framework</span> is a <strong style="color: #b16286">free and open-source web framework</strong> written using Node.js. Serverless Framework is a command line interface.

A <span style="color: #d65d0e">function</span> is merely code, deployed in the cloud, that is most often written to perform a single task.

>[!info]
>Each function is an independent unit of execution and deployment, like a micro service.

A <span style="color: #d65d0e">task</span> can be saving a user to the database or performing a job at a specified time.

<span style="color: #d65d0e">Resources</span> are infrastructure components which the functions use, such as a database (provided cloud provider), or an S3 bucket to store files.

A <span style="color: #d65d0e">service</span> is the Framework's unit of organization, which is configured via a `serverless.yml` file.

<strong style="color: #b16286">Workflow</strong>
- Setup AWS credentials
- Install CLI: <code style="color: #689d6a">$ npm install -g serverless</code>
- Create the AWS HTTP API: <code style="color: #689d6a">$ serverless</code>
- Change the function code
- Deploy: <code style="color: #689d6a">$ serverless deploy</code>
###### <span style="color: #d79921">Serverless Reference Architecture</span>

The Web Application <strong style="color: #b16286">reference architecture is a general-purpose, event-driven back-end</strong> that uses: AWS Lambda, Amazon API Gateway, Amazon DynamoDB, Amazon Cognito and Amazon Amplify Console.

AWS Lambda, Amazon API Gateway are used for its business logic.

Amazon DynamoDB is used as its database and Amazon Cognito for user management.

All static content in the application is hosted using AWS Amplify Console.

The Web Application comprises 3 components, front-end, back-end, and user registration, and authentication.

<strong style="color: #d65d0e">Front End</strong>
- Comprise static content generated by Create React App using: HTML, CSS, JavaScript and Images. All these objects are hosted on AWS Amplify Console
- Downloads resources that run on the client
- Communicates with backend using REST API calls

<strong style="color: #d65d0e">Back End</strong>
- Host logic in lambda functions
- Enables access via API Gateway to frontend
- Stores data in DynamoDB

<strong style="color: #d65d0e">User Registration and Authentication</strong>
- Registers individual users
- Uses Cognito User Pools

<strong style="color: white">Use cases for Serverless application:</strong>
- <span style="color: #98971a">Event streaming</span> <span style="color: #3588E9">--></span> can be written and deployed without setting up-front infrastructure. And can be triggered from publisher, subscriber topics or from event logs, giving elastic, scalable event pipelines without the maintenance of complicated clusters.
- <span style="color: #98971a">Post-processing</span> <span style="color: #3588E9">--></span> Image and Video Manipulation and Image Recognition/AI.
- <span style="color: #98971a">Multi-language</span> <span style="color: #3588E9">--></span> prevent teams from language lock-in.
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
<span style="color: #d65d0e">CI/CD</span> is an automated approach to developing and delivering software with <strong style="color: #d79921">repeatability and reliability</strong>. It's two separate and distinct process that happen right after other.

<span style="color: #d65d0e">Continuous Integration (CI)</span> <span style="color: #3588E9">--></span> is the process of continuously building, testing and integrations every developer change (code) into a repository by using short-lived branches. It ensures that the software continues to work properly after being pushed. The result is potentially deployable code. Examples of CI tools: Jenkins, Circle CI, Travis CI, GitHub Actions.

<strong style="color: white">Benefits</strong> of <span style="color: #d65d0e">CI</span>:  faster reaction time to changes, reduced code integration risk, higher code quality, the code in version control works, master branch is always deployable.

<span style="color: #d65d0e">CI automation</span> <span style="color: #3588E9">--></span> build and test every pull request; use CI tools that monitor version control; tests should run after each build; never merge a pull request with failing tests.

<span style="color: #d65d0e">Continuous Delivery (CD)</span> <span style="color: #3588E9">--></span> is a series of practices designed to ensure that the code can be rapidly and safety deployed to production by delivering every change to a production-like environment. Is the next phase after CI, it prepares the code for release and automates the process that is required to deploy and build the application. Examples of CD tools: Spinnaker, Concourse CI, GitLab, Travis CI, Tekton, GoCD, ArgoCD.
- <strong style="color: white">Best Practices:</strong>
	- Make every change releasable
	- Embrace trunk-based development --> short-lived feature branches
	- Deliver through an automated pipeline
	- Automate as many processes as possible --> to create a good, reliable delivery pipeline
	- Eliminate downtime --> ensure application availability
	- Release at the granularity of test

<strong style="color: white">Benefits</strong> of <span style="color: #d65d0e">CD</span>:  automate software transportation through software development life-cycle (SDLC) stages, reduce deployment time, reduce costs, scale based on project size, deploy code automatically into each stage of SDLC.

<strong style="color: white">Tasks</strong> in <span style="color: #d65d0e">CD pipeline</span>: security scanning, vulnerability scanning, secret scanning, Static Application Security Testing (SAST), Dynamic Application Security Testing (DAST).

Continuous Delivery <strong style="color: #d79921">requires</strong> Continuous Integration.

<span style="color: #d65d0e">CI/CD pipeline</span> <span style="color: #3588E9">--></span> automated process that creates a pipeline of checks.
- <span style="color: #d65d0e">Continuous Integration</span>: <strong>[</strong> <span style="color:#d79921">Plan</span> <span style="color: #3588E9">--></span> <span style="color:#d79921">Code</span> <span style="color: #3588E9">--></span> <span style="color:#d79921">Build</span> <span style="color: #3588E9">--></span> <span style="color:#d79921">Test</span> <strong>]</strong> - <span style="color: #d65d0e">Continuous Delivery</span>: <strong>[</strong> <span style="color:#d79921">Release</span> <span style="color: #3588E9">--></span> <span style="color:#d79921">Deploy</span> <span style="color: #3588E9">--></span> <span style="color:#d79921">Operate</span> <strong>]</strong>
- CD is taking that integrated code(release) and deploying it somewhere.
- CD pipeline: checkout <span style="color: #3588E9">--></span> lint <span style="color: #3588E9">--></span> test <span style="color: #3588E9">--></span> build <span style="color: #3588E9">--></span> deploy
	- lint <span style="color: #3588E9">--></span> run quality checks
	- test <span style="color: #3588E9">--></span> normally involves unit test
	- build <span style="color: #3588E9">--></span> build container image for example

<span style="color: #d65d0e">Continuous Deployment</span> <span style="color: #3588E9">--></span> promote deployment to production (on-prem, public cloud, hybrid cloud), it can be a part of a Continuous Delivery pipeline.

<span style="color: #3588E9">--></span> Code needs to go through several stages of QA and testing to ensure what is delivered to production is fit for purpose.

<span style="color: #d65d0e">DevOps pipeline</span> <span style="color: #3588E9">--></span> workflow that automates software delivery. It is a series of interconnected steps that enable efficient and consistent execution of tasks such as building, testing, deploying, and releasing software.

<strong style="color: white">CI/CD tools:</strong>
- [[Jenkins]], [[GitHub Actions]], [[Gitlab]], [[Tekton]], [[Openshift Pipelines]]
###### <span style="color: #689d6a">GitOps</span>

<span style="color: #d65d0e">GitOps</span> is an operational framework that utilizes the best practices of DevOps.

Also known as Git powered Ops.

Uses shell script for encoding the deployment, and it uses YAML file to describe the desired state.

Leverages Git pull requests to manage infrastructure and application configurations.

Considers Git repository as a single source of truth.

Ensures visibility and audibility.

GitOps advocates to apply principles such as reviews, pull requests, and tagging to infrastructure and application configuration.

<strong style="color:#c6554f">Workflow</strong>
- Devs --> Code Repository --> CI Pipeline --> Build Repository
- SRE --> { IaC Repository - Code Repository } --> { GitOps Agent --> Cloud Resource } --> Build Repository

>[!info]
>The beauty of the GitOps approach is that it eliminates the need for manual intervention while maintaining the security and integrity of the system. The developers or SREs can reverse the process just as easily by simply reverting the Git changes in the IaC repository.

- <strong style="color: white">Principles</strong>
	- Defines system definition as code --> facilitates easy roll-out and rollback
	- Versions and defines desired system configuration
	- Provides git changes that enable pull requests
	- Offers a controller to avoid configuration drifts --> current system state matches desired state
- <strong style="color: white">Benefits</strong>
	- Continuous Deployment --> automation of infrastructure changes
		- Ensures quick and reliable updates
	- Version Control and Traceability
		- Provides a complete history of changes
		- Allows rollback to the previous
	- Consistency and Reproducibility
		- Relies on version-controlled configuration
		- Ensures that actual state matches desired state
	- Collaboration and Review
		- Applies pull requests and code reviews
	- Aubiability and Compliance
		- Provides a centralized and auditable record of modifications
	- Infrastructure as Code
		- Defines and manages infrastructure and configuration

<span style="color:#d65d0e">ArgoCD</span> <span style="color: #3588E9">--></span> declarative Continuous Delivery tool that makes CD easy to automate, audit, and understand. It follows the GitOps pattern of using Git repositories as the single source of truth for defining the desired application state. ArgoCD, as a Kubernetes controller, monitors the current application state compared to the desired state, visualizes the differences, and ensures parity by automatically syncing.
- Argo CD was originally developed by Intuit, as they were looking for a lighter tool than Spinnaker that would improve build and deployment times and streamline their GitOps workflow. The UI is well made and easy to use and integrates well with a variety of CI tools such as Jenkins, GitHub Actions, CircleCI, and more.
- <strong style="color: white">Features:</strong>
	- Declarative application deployment
	- Continuous Monitoring Synchronization
	- Single Sign-On (SSO) Integrations
	- Rollback and Controlled Roll-outs
	- Reusable Application Configurations Patterns
	- Robust Role-based Access Control (RBAC)
## **Micro services**
---
<span style="color: #d65d0e">Microsserviços</span> é uma <strong style="color: #b16286">forma particular de projetar aplicações de software como suítes de serviços implantáveis de forma independente</strong>. 

Surgiu como um movimento de negocio, devido ao desafio de como implantar software mais rapidamente.

O conceito de microsserviços se popularizou com a publicação do artigo de <strong style="color: #d79921">Martin Fowler</strong> em 105 - https://martinfowler.com/articles/microservices.html

Com o modelo de microsservço, cada serviço será empacotando para poder ser implantando de uma forma independente. <strong style="color: #b16286">Cada micro serviço opera de um forma independente</strong>, tipicamente ele é hospedado em um container como elemento de virtualização.

A adoção de uma arquitetura de microsserviços precisa fornecer autônoma técnica para os times. 

>[!info]
>Governança técnica descentralizada é abordagem recomendada para equipes operando com microsserviços.

<span style="color: #d65d0e">modelo conceitual</span> <span style="color: #3588E9">--></span> https://github.com/dotnet/eShop

<span style="color: #d65d0e">proteção modular</span> <span style="color: #3588E9">--></span> arquitetura com baixo acoplamento e alta coesão

<strong style="color: white">Razões para uso:</strong>
- custo elevado de aplicações com arquitetura monolítica para alterar e implementar em produção
- servidores web e de aplicação compartilhados com outras aplicações
- longos ciclos de mudança
- dificuldades de implantação
- custo de evolução do legado

A <strong style="color:#689d6a">Monolithic</strong> application has all or most of its functionality within a single process. And the application is managed in internal layers or libraries. The layers are tightly connected and dependent on each other,

Monólito não é um código ruim, é apenas um código que é implantado com um único bloco num ambiente de produção, isso muitas vezes dificulta para que esse processo seja rápido.

<strong style="color: white">Benefits</strong> of Monolith: simple and less cross-cutting of features and functionalities

<strong style="color: white">Drawbacks</strong> of Monolith: with growth, complexity increases; less flexibility to adapt to new technology.

<span style="color: #d65d0e">estrangular monólito</span> <span style="color: #3588E9">--></span> mover de um monólito para uma arquitetura de microsserviços.

<span style="color: #d65d0e">Windows Forms Application</span> <span style="color: #3588E9">--></span> typical example of a Monolithic design.

<span style="color: #d65d0e">Plataforma CNCF</span> (Cloud Native Computing Foundation) <span style="color: #3588E9">--></span> fornece uma controladoria de mais de 1000 tecnologias organizadas em domínios.
##### <span style="color:#d79921">Características</span>

Serviços como componentes (ao invés de bibliotecas) são publicados de maneira independente.

Os serviços precisam denotar capacidade de negocio (ex: gestão de pedidos)

Interface Publicadas (APIs) <span style="color: #3588E9">--></span> <strong style="color: #b16286">representa um sub conjunto das interfaces dentro de uma aplicação</strong>, ela é versionada e possui um endpoint que registra o local daquele interface (conceito mandatório).

>[!info]
>Uma interface publicada da mais controle para que se possa mexer em várias partes da aplicação sem impactar outras partes. A utilização de APIs como REST, RPC ou GraphQL vai habilitar um conceito de uma interface publicada.

base de dados próprias <span style="color: #3588E9">--></span> flexibilidade, proteção modular, menor acoplamento.

implantação automatizada

>[!note] <strong>Obs:</strong> 
>Microsserviços implicam em uma agenda DevOps (pipeline automatizada, compenentes hospedados em conteineres - Docker).

inteligência nos endpoints (APIs) <span style="color: #3588E9">--></span> único ponto de contato para alguém ler ou enviar informações ou comandos para um micro serviço.

controle descentralizado de linguagens (linguagem poliglotas) e de base de dados (persistência poliglota)
##### <span style="color:#d79921">API Gateway</span>

API Gateway em arquitetura possui dois significados: 
- padrão arquitetural que irá isolar o front do back; 
- produto de mercado que irá implementar esse padrão arquitetural. 
- <strong style="color: white">Exemplos</strong> de produtos de mercado: API G, Amazon API Gateway, etc..

<strong style="color: white">Papel do gateway:</strong>
- <span style="color: #98971a">segurança</span> <span style="color: #3588E9">--></span> separando um rede desmilitarizada de internet da rede militariza, onde terá IP privativos dentro de um endereçamento de rede proprietário, controle de acessos, observabilidade e auditoria dos acessos, mecanismo ligados a monetização.

O API Gateway pode fornecer a cada tipo de aplicativo cliente, interfaces próprias chamadas de <span style="color: #d65d0e">BFF (Backend for frontend)</span> <span style="color: #3588E9">--></span> padrão arquitetural muito usado em microsserviços quando se expõe um conjunto particular de endpoints para uma aplicação.

Microsserviços podem chamar outros microsserviços através de RPC, chamadas ligadas a rest. 

Em arquiteturas de larga escala é mais comum que se utilize arquitetura orientada por eventos <span style="color: #3588E9">--></span> tem se a figura de um servidor de fila de mensagens ou de streaming que ira fazer a comunicação assincronia entre mensagens dos vários microsserviços.
##### <span style="color:#d79921">Padrões Arquiteturais</span>

Padrão arquitetural é uma melhor prática, é algo que foi descoberto no mercado e que se tornou uma melhor prática para se lidar com um certo problema que emerge em um determinado domínio.

Todo padrão possui uma linguagem comum para descreve-lo (Contexto, Problema, Solução).

<span style="color: #d65d0e">Plataforma web</span> <span style="color: #3588E9">--></span> microservices.io/patterns

Quando uma grande coleção de padrões são combinados tem-se uma linguagem de padrões.
##### <span style="color:#689d6a">Twelve-factor</span>

The Twelve-factor app methodology is suited for web apps, and it's frequently used with microservices.

The twelve factors can be grouped according to these phases of the software delivery life cycle: <strong style="color: #d79921">Code</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Deploy</strong> <span style="color: #3588E9">--></span> <strong style="color: #d79921">Operate</strong>

<strong style="color: #d79921">Code factors</strong>

- <strong style="color: #98971a">Factor 1</strong>: <span style="color: #d65d0e">Codebase</span>
	- Track in a version control system (VCS)
	- Maintain one-to-one relationship between code base and app
	- Deploy multiple instances of the app
	- Develop different versions of the code base in each deploy
- <strong style="color: #98971a">Factor 5</strong>: <span style="color: #d65d0e">Build, relsease, run</span>
	- Build: Transform a code base into an executable unit called a build
	- Release: Combine build with configuration do that it's ready for execution
	- Run: Run the application
	- <span style="color: #3588E9">--></span> All three stages should be strictly separated
- <strong style="color: #98971a">Factor 10</strong>: <span style="color: #d65d0e">Dev/prod parity</span>
	- Minimize differences between development and production
	- Use same backend services across environments
- <strong style="color: #98971a">Factor 2</strong>: <span style="color: #d65d0e">Depedencies</span>
	- Assume an app is only as reliable as its reliable dependency
	- Explicitly declare any dependencies

<strong style="color: #d79921">Deploy factors</strong>

- <strong style="color: #98971a">Factor 3</strong>: <span style="color: #d65d0e">Config</span>
	- Keep everything that varies between deploys such as credentials and backend service locations in config
	- Keep separate from the code
	- Store config in environment variables
- <strong style="color: #98971a">Factor 4</strong>: <span style="color: #d65d0e">Backend services</span>
	- Do not distinguish between local and third-party services
	- Access all services by a URL and credentials so they can be swapped without changing the code
- <strong style="color: #98971a">Factor 6</strong>: <span style="color: #d65d0e">Processes</span>
	- Should be stateless and share nothing
	- Do not share memory and file systems
	- Store persistent data in a backend service
	- Store data centrally
- <strong style="color: #98971a">Factor 7</strong>: <span style="color: #d65d0e">Port biding</span>
	- Export services by port biding
	- Export HTTP and other services
	- Declare a web server library as a dependency
	- Apps accessible via a URL, become backend services for other apps

<strong style="color: #d79921">Operate factors</strong>

- <strong style="color: #98971a">Factor 8</strong>: <span style="color: #d65d0e">Concurrency</span>
	- Scale an application
	- Stateless processes can be spun up without creating dependencies on other processes
- <strong style="color: #98971a">Factor 9</strong>: <span style="color: #d65d0e">Disposability</span>
	- Require minimal process start time and graceful termination
	- Quickly deploy code or config changes
	- Easily scale apps
- <strong style="color: #98971a">Factor 11</strong>: <span style="color: #d65d0e">logs</span>
	- App should not concern itself with storing logs
	- Treat logs as an event stream
	- Execution environment captures, aggregates, and routes logs to their destination
- <strong style="color: #98971a">Factor 12</strong>: <span style="color: #d65d0e">Admin processes</span>
	- Enable one-off app management processes
	- Run against a release, using same code base ad config
	- Part of application code
##### <span style="color:#689d6a">Microservices</span>

<strong style="color: #d79921">Microservices architecture</strong> is an approach in which a single application is composed of many loosely coupled and independently deployable smaller services. These services typically have their own technology stack, inclusive of the database and data management model.

>[!note]
>Microservices architecture is an application-scoped concept. 
>Example: E-commerce application, that can have separate microservices to process orders, security, and analytics.

One of the <strong style="color: #d79921">key elements</strong> of a microservice is that it <strong style="color: #b16286">is generally small and isolated in terms of computational resources</strong> for each running instance.

Application components can be developed and updated more efficiently by multiple developers working independently. Teams can use different stacks and runtime environments for different components.

<strong style="color: #b16286">Microservices break down large applications into their core functions</strong>. For example: Search, Recommendations, Customer Ratings, or Product Catalogs. Each is developed independently of one another, yet work together on the Cloud development platform to create a functioning application.

For each microservice to find each other, they do this by using something called <span style="color: #d65d0e">Service Discovery</span>, which creates a road-map for these and many other microservices to communicate. When microservices find each other, they communicate using an application programming interface or an API.

Teams can even choose different programming languages for different components as they are dependent on each other via an API endpoint.

Microservices components communicate with one another over a combination of REST APIs, event streaming, and message brokers, and they are segregated and organized by business functionality.

The components can be scaled independently of one another, reducing the waste and cost associated with having to scale entire applications because a single feature might be facing too much load.

>[!note]
>Scaling of microservices, it usually involves horizontal scaling.

Microservices require less infrastructure because they enable precise scaling of only the components that require it.

Like SOA, <strong style="color: #d79921">microservices architectures</strong> comprise loosely coupled, reusable, and specialized components that often work independently of one another.

Even the data in a micro service is not shared with other services.

<strong style="color: white">Benefits</strong> of Micro services: easy of development, flexibility to add new technology.

<strong style="color: white">Drawbacks</strong>: security requirement, debugging is a challenge.
###### <span style="color: #d79921">Microservices Patterns</span>:

<span style="color: #d65d0e">Single-page application (SPA)</span>:
- Enabled but more powerful browsers, faster networks, and client-side languages
- Loads one interface that never reloads
- Updates dynamically using calls to backend REST-based services
- Simplifies the front-end experience
- Places greater performance responsibility on backend services

<span style="color: #d65d0e">Backend for Frontend (BFF)</span>:
- Provides superior support compared to a generic backend
- Inserts a layer between user experience and the resources
- Enables customized user experiences for different channels
- Supports one backend type per user interface

<span style="color: #d65d0e">Strangler</span>:
- Manages refactoring in stages
- Gets its name from a vine that strangles a tree
- Splits functional domains
- Replaces with nre microsservice per domain
- Enables two applications to exist side-by-side

<span style="color: #d65d0e">Service discovery</span>:
- Helps applications and services discover each other
- Provides flexibility as service instances can change dynamically
- Could be used by load balancers to perform health checks and rebalance traffic on service failures
##### <span style="color:#689d6a">IBM Cloud Engine</span>

Is a platform for deploying your microservices.

“<span style="color: #d65d0e">Code Engine</span>” abstracts the operational burden of building, deploying, and managing workloads.

IBM Cloud Code Engine can be seen as a <strong style="color: #b16286">fully managed, serverless platform</strong>. It combines all features that are required by <span style="color: #d65d0e">Platform as a Service (PaaS)</span>, <span style="color: #d65d0e">Containers as a Service (CaaS)</span>, and <span style="color: #d65d0e">serverless deployment models</span>.

IBM Cloud Code Engine runs workloads, including microservices, web apps, event-driven functions, or batch jobs.

<strong style="color: #d79921">Use cases</strong>:
- Deploy application to Code Engine
- Pushing the source code directly (Build and Deploy)
- Create and Run batch jobs

<strong style="color: white">Benefits:</strong> Focus on the code, Go live in seconds, Auto-Scale, Control access, Secure private network, Integrates with other IBM Cloud services.

<span style="color: #d65d0e">Project</span> <span style="color: #3588E9">--></span> represents a group that contains and manages its resources and entities

A <span style="color: #d65d0e">grouping</span> in Code Engine <strong style="color: #b16286">contains entities</strong> such as build, app, job, and certificate for Transport Layer Service (or TLS) HTTPs connections, and so on.

One important function of a project is providing a <span style="color: #d65d0e">namespace</span> for its entities. Another important function is managing resources and providing access control.

<span style="color: #3588E9">--></span> Names of <span style="color: #d65d0e">entities</span> <strong style="color: #b16286">need to be unique within a namespace</strong>, but not across namespaces.

In Code Engine, the code will run the application.

An application runs the code to server HTTP request or to create Web Sockets sessions.

>[!info]
>Web Socket is a communication protocol based on Transmission Control Protocol (or TCP). It is mostly used for long-running and session-based communication between clients and servers, such as a chat application.

<span style="color: #d65d0e">Buid</span> <span style="color: #3588E9">--></span> mechanism than can be used to create a container image from a source code.

The Code Engine supports building from a <span style="color: #98971a">Dockerfile</span>. Alternatively, it can use a <span style="color: #98971a">Cloud Native Buildpack</span>.

>[!note] 
>build pack is another popular way to build the container image. It contains executable to perform tasks such as inspecting source code, creating a build plan, or executing the build plan to produce an image.

<span style="color: #d65d0e">Job</span> <span style="color: #3588E9">--></span> one-time execution of your code. It runs executable code, and depending on the workload, the Code Engine will create one or more instances of a job.

<span style="color: #3588E9">--></span> jobs are designed to run one time and exit.

<strong style="color: #d79921">Typical jobs</strong>: Data Processing Job, Machine Learning Training Job, Reporting Job, Billing Job.

To update an application, the <span style="color:#98971a">IBM Cloud Console</span> can be used. But for more complex and precise application updates, the <span style="color:#98971a">Code Engine CLI</span> is more appropriate.
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

start by importing the when and then decorators from Behave. Since you don’t use the Given keyword in the feature file, you don’t need to import the Given keyword decorator here. Ex: `from behave import when, then`

<code style="color: #689d6a">context</code> <span style="color: #3588E9">--></span> variable passed into every step definition
- exists for the entire feature file
- is useful for passing information between steps

<span style="color: #d65d0e">variable substitution</span> <span style="color: #3588E9">--></span> makes the steps more generic
- minimizes the number of steps
- leads to greater reuse
- Ex: `@when('I copy the "{variable_name}" field')`

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
###### <span style="color: #98971a">Selenium</span>

Selenium is a collection of tools for automating web browser activity

At its core, Selenium is a WebDriver, an interface to write instruction sets that you could run interchangeably across popular browsers like Chrome, Firefox, Safari, and Edge.

With only a few lines of code it interacts with browsers just like real users would. You could enter data into fields, read data back from fields, click links, click buttons, everything a real user can do.

Works perfectly for integration testing of multiple microservices that share a common user interface.

Initialize Selenium
1. Ensure the web rower is installed
2. Instantiate the driver

To use Selenium, you must first tell it which element on the HTML page you want to interact with. Selenium can find elements by Class name, CSS selector,  ID, name, XPath, link text, partial links text, tag names.

Selenium for Python has function calls for each of these selectors.
- Ex: `find_element(By.ID, element_id)`
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

>[!info]
>Monitoring is a routine, ongoing process, and it is an operational-level activity. It’s usually performed by developers and their teams.

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

>[!info] 
>Is a business-level activity, and it is usually performed by others not involved in developing the application (managers, supervisors, or external independent parties).

Is an assessment of whether a solution meets its stated goals.

It's determined at the design stage or when the solution was implemented

Anticipated and unanticipated outcomes

Can show how useful an app is and how sustainable and profitable it is.

Is an important part of the <strong style="color: #b16286">monitoring process</strong>
- Monitoring ---> Performance ---> Solution
<br>
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

<span style="color: #98971a">Latency</span> <span style="color: #3588E9">--></span> measures the time between when a request is sent and when a request is completed
- successful and failed requests both have latency!!
-  longer latency times --> may indicate slower connection errors
- include error latencies along with all other latencies

<span style="color: #98971a">Traffic</span> <span style="color: #3588E9">--></span> indicates demand for service
- helps fine-tune user experience
- show storage system traffics
-  measures web app traffic
- viewable by page or resource

<span style="color: #98971a">Errors</span> <span style="color: #3588E9">--></span> proactively fix errors
- fix failed requests and requests completed incorrectly
- define critical errors
- understand the system's health
- track erros: servers, client, incorrect content

<span style="color: #98971a">Saturation</span> <span style="color: #3588E9">--></span> measure the percentage of use of a system
- Ex: Memory and CPU resources usage
- --> optimize the services
- set a utilization target
- recognize latency and saturation indicators
##### <span style="color:#d79921">Components of monitoring</span>

<span style="color: #98971a">Metrics</span> <span style="color: #3588E9">--></span> represent resource usage or behavior data that can be observed and collected throughout the system
- low-level usage summaries to higher-level, specific data
- total capacity of a component
- view of behavior and health of system
- understand trends
- correlate diverse factors
- measure change in performance, consumption, and error rates
- <strong style="color: white">Types of Metrics</strong>
	- <span style="color: #98971a">Host-based</span> <span style="color: #3588E9">--></span> measure cpu, memory, disk space and processes
		- indicators are anything involved in evaluating the health and performance of an individual machine
		- comprised of usage or performance of the operating system or hardware
	- <span style="color: #98971a">Application</span> <span style="color: #3588E9">--></span> units that depends on resources like services or apps
		- indicators of health, performance, and load
	- <span style="color: #98971a">Network and connectivity</span> <span style="color: #3588E9">--></span> indicators of availability
		- signals of accessible services
		- show fundamental correctness and delivery: connectivity, error rates and packet loss, latency and bandwidth utilization
		- availability and responsiveness
	- <span style="color: #98971a">Server pool</span> <span style="color: #3588E9">--></span> collections of machines
		- similar to machine-level apps and server metrics
		- summarizes the health of a collection of servers

<strong style="color: #C6554F">Obs:</strong> monitoring external dependency metrics helps with identifying problems that may affect the operations

<span style="color: #98971a">Observability</span> <span style="color: #3588E9">--></span> analyzing data to improve awareness of the component characteristics and behavior.
- includes recognizing and understanding patterns between data collected, aggregated information, and resources and values across services.

<span style="color: #98971a">Alerting</span> <span style="color: #3588E9">--></span> responsive component of a monitoring system that performs actions based on changes in metric values.
- based on metrics and action
- allows admins to disengage from the system
- defined situation and passive monitoring
- programmatic responses
- bring human attention to the status of systems

>[!info]
><span style="color: #3588E9">--></span> <strong style="color: #b16286">Ideal monitoring systems</strong> are independent, easy-to-use and relibale, maintained data, and data correlation from different sources.
##### <span style="color:#d79921">Synthetic Monitoring (SM)</span>

It's also called synthetic testing or proactive monitoring.

Synthetic monitoring is a method used to keep track of how well an application or website is performing --> involves creating a set of predefined actions or requests that a user would typically make on the website or application.

The actions are recorded and replayed periodically --> tracks simulated user interactions/transactions (scripts).

It uses predictive behavior to understand user experience and improve website performance.

It runs tests to provide information on essential business operations, application availability, website speed, and other factors.

--> The goal is to ensure application/service is up and running -- identifies and resolves immediate problems.

It envolves other computers or checkpoints.

The synthetic transaction monitor measures: availability and responsiveness (in milliseconds) of the resource over time.

Synthetic monitors
- Operate like bots
- Check website's working and performance
- Use network of checkpoint
- Checkpoint at different parts of network or world

Process:
- Record ---> Check result = Error ---> New test required
- Alert for confirmed error

Importance
- Quicker problem resolution
	- instant access to reports
	- teams find cause --> implement fix
- Alerting
	- should be trigger before experiencing problems
	- effective proactive approach
	- checks and verifies details
- Moderating other content
	- third-party
	- allows holding third-party vendors accountable
- SLAs compliance
	- detailed reports
	- exact availability percentage

Tools:
- Solutions to verify: performance, availability, reachability and reliability of an app/wesbite.
- Used for benchmarking and baselining, gettings ready for heavy traffic, monitoring complex transactions and business processes, meassuring and adhering to SLAs.
- Datadog, Semtext, AppDynamics, Dynatrace, New Relic, AlertBot, Uptrends.
- Features:
	- Captures business transactions
	- Measures and compares performance experiments
	- Robust alerting and notification
	- Benchmarking and comparison

##### <span style="color:#d79921">Application Monitoring</span>

Is a process that developers use to ensure their software performs as intended.

Allows rapid detection of issues, bugs, or unexpected events - real time.

Provides better understanding of app usage.

Deployed on-premises of from cloud.

Hardware-based appliances or software-based solutions.

Software-based agents connect to applications runtime APIs to collect data.

Works in conjunction with synthetic traffic.

Monitoring provides valuable insights, which help enable customer satisfaction and drive business growth.

Application monitoring can help maximize the application’s availability and performance.

<strong>Steps for implementing</strong>
- identify monitoring goals --> Choose a monitoring tool --> Define the Key metrics --> Instrumentation (App Code) --> Set up alerts --> Data storage and visualization --> Test and validate --> Continuous improvement

Benefits: rapid diagnosis, faster resolution, improved productivity, accelerated deployment, improved experience.

Essential aspects:
- Performance monitoring --> track metrics, receive notifications from metrics.
- Availability monitoring --> available to users, checks uptime and downtime, verifies reponsiveness.
- Error monitoring --> track errors and exceptions, identifies bugs or issues in code, capture stack traces, provides informatiom about root causes of error.
- Log monitoring --> analyzes log generated by the app
- User experience monitoring --> how users interact with the app, relevant metrics to measure customer satisfaction: user actions, sessions durations, conversion rates.
- --> All of the aspects helps to determine the best-suited approach to implement application moniroting.

Functions:
- Observation of components --> essential to ensure that the app and its dependencies are running smoothly and as intended.
- Visualization and alerts --> Dashboards provide an overview, and alerts call attention to specific problems.
- Detection of anomalies --> varying from simple threshold detection to advanced machine learning pattern recognition.
- Distributed tracing --> developers can monitor how one event connects across multiple nodes to detect the origins of errors
- Dependency mapping --> visually represents how requests travel between services.

Telemetry --> system data automatically gathered and recorded for monitoring.
- includes resource utilization, server logs, network traffic, and performance metrics.

APM tools
- Systematically collect and analyze data
- Provide real-time insights into the application behavior
- Track key performance indicators (KPIs)
- Detect anomalies and troubleshoot issues
- Visually depict the events' connection
- Maximize application availability
- Primary functions:
	- Observe app components: Servers, Database, Message Queues
	- App dashboards and alerts: overview and specific problems
	- Dependency and flow mapping: Visually depict how requests move between services
	- Detect anomalies: Threshold detection, Avanced machine learning pattern recognition
	- Distributed tracing: Track how one event connects across multiple nodes, Detect the origin of errors
	- <strong>Important factors for choosing the right APM tool:</strong>
		- Functionality
		- Scalability
		- Integration capabilities
##### <span style="color:#d79921">Visualization</span>

Is the graphical representation of information of data collected from the business infrastructure that helps to understand and maintain the application’s performance.

Visual elements: charts, graphs, maps.

Essential for analyzing large amounts of data.

>[!note]
>Operational insight gives DevOps staff a deeper understanding of IT infrastructure and business systems

--> It can represent massive amounts of data in a way that allows an operator to spot any trends or problems quickly.

Benefits:
- Operational visibility provides deeper understading of IT infrastructure and business systems in real time
- Rapid absorption of information for improving insights and quicker decision-making
- Eliminate debugging and increase understanding of next steps taken for improving application
- Easy distibuition of inofrmation increases opportunity to share insights with everyone involved

Components:
- Dashboards used for visualization
- Dashboards contain indicators for systems and performance
- Visual elements include charts, graphs, timelines, and illustrations
- Customizable
- Configurable

Types of data visualization:

>[!note]
>The right visualization must be paired with the right set of information in order for the visualization to be the most effective and impactful

- Bar graphs and pie charts,
- Tables, Maps, Infographics, Dashboards,
- Line charts -->
- Area charts -->
- Scatter plots -->
- Tree maps -->
- Population pyramdis -->

Product types:
- Free or open-source, like Kibana and Elasticsearch
- Proprietary, like SysDig and Splunk
- Cloud solution, like IBM Cloud, Amazon AWS, Microsoft Azure, and Google Cloud

Tools:
- Kibana --> open-source web application that’s often used in conjunction with Elasticsearch.
	- Elasticsearch --> open-source search and analytics engine that allows to store, search and analyze large volumes of data.
	- provides a user interface for managing authentication and authorization requests for Elasticsearch.
	- Kibana allows to visualize, search, and analyze data
- Splunk --> proprietary solution.
	- used to monitor, search, analyze and visualize big data
	- combines log analysis and visualization of data collected from: Web applications, Sensors, Devices.
	- it can also analyze any structured data or semi-structured data with data modeling
##### <span style="color:#d79921">Alerting</span>

Critial part of monitoring

Reponsive element of a monitoring system

Helps detect and address issues before user are impacted.

Proactively notifies when monitoring detects issues.

Can trigger actions based on changes detected.

How it works
1. Collection of data and metrics
2. Analysis of data collected
3. Detection of failure or anomaly & alarm raised and sent
4. Investigation, mitigation, and resolution of issue
5. Continuation of monitoring

Alerting process:
- Alarm triggered
	- alert is sent
- Mitigation success
	- caused identifies and mitigated
	- mitigation puts system back in equilibrium
	- alarm is cleared
- Mitigation fails
	- raise question about mitigation efficacy
	- may require an alternate strategy to resolve issue

Types of alerts:
- Metric alerts --> based on raw data collected
	- provide information about the availability of resources on systems, applications, databases, and web servers.
	- System health.
	- Usage trends --> to understand the effects of any changes
- Log alerts --> different from metric alerts
	- use log analytics queries to evaluate resource logs at predefined intervals to see how the apps or services are, and have been performing.
	- provide a trail of events (for troubleshooting)
- Activity log alerts --> automate the log review process
	- use rules and conditions.
	- triggered when a new event matches the defined rules or conditions.
- Smart detection --> works with Application Insights
	- analyzes telemetry sent by the app to warn of potential performance, and failure anomalies detected in the web application.
	- Alerts are sent automatically if sudden changes are detected.

Best practices:
- After issue is resolved, tithen alerting configurations to prevent recurrence of costly outages.
- Reaevaluate baseline and adjust respective mionitors to imrpove detecability of real issues.

Benefits:
- Sport problems anywhere
- Identify troubled device, apps, and systems
- Eliminate manual log review
- Define scenarios for active and passive monitoring
- Respond quickly to issues

Open-source tools: Bosun, Cabot, StatsAgg.
##### <span style="color:#98971a">Prometheus</span>

It is an open-source monitoring, and alerting solution built by a company called SoundCloud. Prometheus monitors servers, virtual machines (or VMs), and databases. It analyzes, tracks, and reports system health, application behavior and prediction, and performance.

Provides detailed, actionable metrics using a robust data model and query language.

Instrumentation, client libraries, and exporters are used to capture metrics from data sources.

How Prometheus works
1. Automatic discovery of services
	1. Or manually define targeted service to monitor
2. Prometheus send HTTP request from HTTP/HTTPS endpoints
3. Metrics, unique identifiers, and timestamps pulled
4. Data is collected, organized, compressed, stored in time-series database
5. View data in Dashboards with PromQL and use ot send alerts to Alertmanager

Architecture
- Autonomous servers - don't rely on distributed or networked storage
- Cloud-based or on-prem
- Scrapes metrics from the persistence layer --> acts as an intermediary between the business functions of the application and the data it stores in a relational database.
- Some Prometheus implementations can use a dedicated time-series database to store Prometheus data.
- It uses a time-series database to simplify the taking of incremental backups of monitoring data.
- --> Prometheus provides native support to some services (no monitoring agents).

Alertmanager --> flexible metrics collection and alerting tool.
- used with Prometheus
- handle alerts and sends notifications

Benefits:
- Collect and evaluate metrics for numeric time-series data
- Multidimensioanl data collection and querying
- Machine-centric monitoring and service-oriented architectures
- Collects millions of metrics per second
- Is typically used in combination with Grafana
##### <span style="color:#98971a">Grafana</span>

Is a professional cross-platform, open-source data visualization and metrics analysis tool --> provides time-series analytics.

Can be used to query, visualize, alert on, and understand metrics no matter where the data is stored.

Transforms time-series databases (TSDB) into graphs and visualizations.

Facilitates comprehension of massive amount of monitored data.

Commonly used with Prometheus

How it Works
1. Deploy and create connection to data source or database & configura alerts and notifications
2. Retrieve metrics from database
3. Visualize, analyse, alert, and report
	1. Optional: Set up Reporting feature

Architecture
- Browser-based UI --> cloud-based or on-prem
- Only works on data stored in databases --> no data collection
	- connects to a data source retrieves metrics
- Custom dashboards facilitate comprehension
- Native support for dozen of databases: Microsoft SQL, AWS CloudWatch, Prometheus, ElasticSearch and others

Benefits:
- Integrates all data sources into one single, organized view.
- Helps guide business decisions with powerful analytics.
- Tracks user nd application behavior, error frequencies, and types.
- Gain a deeper understanding of the application and infrastructure performance.
- Browser-based data accessible by entire team.
- Fosters a data-driven culture in organizations.

Features: visualization of data, fully customizable panels, open-source community, alerts, explore logs and data more efficiently, manageability.
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

Syslog Monitoring software is designed to compare real time metrics with historical metrics to offer a comprehensive understanding of a network's performance over time.

<strong style="color: #d79921">Why use it</strong>
- Diagnostics
	- Correlating trakced information. Ex: customer transactions, security threats, timeouts, and consumer behavior.
	- Diagnose issues
	- Identify and resolve bugs in a production environment
- Auditing
	- Significant events
	- Information on management and finance
	- Business requirement

Log formatting
- Choose a logging library --> Define log levels --> Format message --> Output Logs --> Test and refine

Log structuring
- enable standardized log formats for effortless, parsing, querying and analytics.
- JSON - De fato standard for structure logging
- --> consider using key value pairs, XML, or another format
- review the supported formats for auyomatic parsing
- benefits:
	- easy querying and filtering of log data
	- efficient stirage and processing
	- better bisibility into system behavior

Common features in logging frameworks
- local levels: DEBUG, INFO, WARNING, or ERROR
- log messages: Timestamp, Severy Levels, Other relevant details
- destination: where are logs to be sent

Log monitoring tools
- Performs essential event log monitoring tasks
- Detects suspicious activity as soon as it occurs
- Uses related log data to uncover root sources
- Troubleshoots efficiently
- Generates alerts and reports
##### <span style="color: #d79921">Types of applications logs</span>

Event logs
- record application events and user actions
- useful for troubleshooting issues
- detecting security breaches

Error logs
- record error messages
- contain information about exceptions, stack traces, and error codes
- diagnose and fix problems

Access logs
- record information about user access
- audit and monitor user activity

Performance logs
- track metrics related to the performance of the application
- useful for identifying, bottlenecks and optimizing performance

Debugging logs
- contain detailed information about variables, method calls, and other debugging data
- trace program flow and identify bugs
##### <span style="color: #d79921">Logging Tools</span>

Mezmo --> earlier known as LogDNA
- Is an observability platform for managing and taking action on the telemetry data
- Mezmo log analysis enables businesses to ingest all their log data to a single platform, normalize it, and route it to the appropriate teams so that they can take meaningful action in real-time.
- Logs can be centralized using Mezmo agents, code libraries, or APIs
- Mezmo's log analysis platform lets you collect, monitor, parse, live tail graph and analyze logs with clear visualizations and smarter alerting all within minutes.
- Your organization is an independent workspace where you can access and configure your logs, add members, change billing plans, and manage other aspects of your account.
- search term is a string consisting of a single word or a phrase surrounded by quotes --> search capability
- Views can have multiple alerts and multiple alert types.
- With spike protection features, you can set dynamic thresholds and alerts when data volume limits are hit
- Mezmo provides several methods for ingesting log data. You can install the Mezmo log agent directly on the host where your logs are generated. You can deploy the Mezmo agent on Linux, Windows, MacOS, Kubernetes, and OpenShift systems
- With the Mezmo CLI, you can live tail and filter logline data. The Mezmo client-side logger sends logs from your client-side JavaScript application to Mezmo's ingestion servers
- You can use the Mezmo API to send log lines to Mezmo, as well as programmatically manage to start and stop ingestion.
- Features
	- Automatic and custom parsing to easily surface data from logs
	- Notifications about system activity
	- Notify teams of production issues
	- Configure using PagerDuty and Slack
	- Ability to see critical event
	- Visualize log data over some time
	- Set dynamic thresholds and alerts
- Benefits:
	- centralize log data, 
	- automatic and Custom Parcing, 
	- powerful exclusion rules, 
	- configurable alerts, 
	- spike protection features, 
	- archive log data.

Sumo Logic --> cloud-based solution
- Offers log monitoring and analytics features
- Facilitates application and infrastructure monitoring in mulit-cloud setups
- Proactive resolution of issues in CI/CD pipelines.
- Analyzes and correlates events and data across multiple logs in real-time
- Features:
	- Unified platform for all logs and metrics
	- Advanced analytics powered by machine learning and predictive algorithms
	- Quick an easy setup
	- Assistace for high-resolution metric
	- Option of multi-tenant or single instance to serve group of users

IBM Instana Observability --> fully automated APM solution
- Manages microservice and cloud-native applications
- Automatically makes the application and services visible
- Enables taking intelligent action based on available information
- Benefits:
	- Monitor and analyzes: Applications, Services, Infrastrcuture, Web browswrs, Mobile Application and more.
	- Diplay real-time data through distributed tracing and 1-second metrics.

Datadog --> offer visibility into cloud-state infra
- Aggreagtes, tags, and stores metrics and events
- Collects, seraches, analyzes, and correlate logs.
- Benefits:
	- Correlate individual logs and detect patterns
	- Visually data using customizable, drag-and-drop dashboards.
	- Perform log querying without knowing any query language
	- Alerts driven by machine learning
##### <span style="color: #d79921">Log Storage</span>

>[!info]
>it's recommended to store log data for a minimum of one year to facilitate future investigations if needed. When storing logs, you can choose to backup data to on-premises servers or in the cloud.

observability --> means to accomplish real business objectives
- can be achieved by storing log data

log data helps to improve the reliability of the systems, determine the need for increased capacity and identify sluggish queries, erros that prolong transactions, or bugs

maintain security posture of environments --> indicate a potential ongoing cyber attack; send prompt alerts and automatic responses

improve IT system' decision-making
- user behavior analytics
- users' achievement of objetives

auditing
- application events
- management/finance information
- business requirements

Storing log in clouds
- scalable storage capacity
- stable retrieval speed
- Ex: Amazon S3 ---> employees AES-256 encryption

Log retention - Dimensions
- Criticality
	- varied retention policies based on the significance of different parts of the system
	- critical components - long retention periods
- Security
	- applications with sentive data and high-risk processing - Extended retention policy
	- beahvior tracking services for app improvement - No extended retention policy
- Maturity
	- Limited ongoing feature development
	- Short retention policy to reduce storage costs
- Frequency
	- Applications running infrequently benefit from extended retention policies
	- Trace back in time due to infrequent execution for debugging
- Cost-effectiveness
	- project's cost compatibility
	- data generation and storage express
- Discovery and resolution
	- average time to identify and fix problems
	- sufficient space for effective debugging

- Best practices
	- define what to log
	- use a centralized logging system
	- choose and appropriate storage solution
	- set up log rotation
	- implement access controls
	- regularly review and analyse log
	- retain logs according to legalor compliancd requirements
- Tools:
	- Elasticsearch --> distributed RESTful search and analytics engine that can be used for storing and analyzing logs
	- Splunk --> software platform used for searching, monitoring and analyzing machine generated big data via a web style interface
	- Graylog --> open-source log management platform that collects, indexes and analyzes structured and unstructured log data
	- Logstash --> tool by Elastic used for collecting, parsing and storing logs for later use with Elasticsearch
	- Fluentd --> open source data collector designed to unify logging infrastructure
	- Sumo Logic --> cloud-based log management platform that allows users to ingest, analyze and visualize logs in real time
##### Parsing logs

extract meaningful information from logs

converts log files into a readable format

simplify filtering, analysis, and manipulation of information

--> A log management system must parse the files to extract meaningful information

log parsers are built into the log management software's engine

Most log management solutions have the builtin parser for common data types like Windows event logs, JSON, CSV, or W3C

Parsers are configured to recognize these log types based on the source data structure and file extensions.


Steps to parse logs
- Identify the format of the log files ---> Determine the relevant fields in log files --> Choose a tool or library ---> Write code to read data and extract fields ---> Store the extracted data in a structred format

Steps to parse log:
- Identify the relevant data --> Define a consistent format for logging --> Add structured log statements in the codebase --> use a logging library or tool to collect and analyze the structured logs
##### Distributed logging

--> a technique used in computing systems to collect and store log data from multiple sources across different nodes or servers

identifies overall issues with a system

centralized monitoring analysis of system performance

determines the root cause an issue and fix it

analyze and trouybleshoot issues across a distributed system easily

Implementation
- ( Choose a logging framework ) --> ( Configure the logggers to send log events to a centralized location ) --> ( Include relevant information in logs ) --> ( Set up a centrlized logging server ) --> ( Define log retention policies ) --> ( Monitor the logs )

##### Distributed tracing 

 the practice of tracking a single request or transaction as it moves through a distributed system.
 
tracks individual requests through the system

identifies performance bottlenecks and errors

monitors service dependencies

correlates all the logs and metrics

provides end-to-end visibility into the entire system

Important Concepts
- Trace --> a collection of spans representing a single logical request or workflow
- Span --> represent a single operation within a trace
	- it has a start and end time and may include metadata such as the name of the service performing the operation, and ID for the operation, and any tags that provide additional context.
- Trace ID --> unique identifier for an entire trace
	- all spans belonging to the same trace have the same trace ID
- Parent/Chid relationship --> one span calls another span as part of its operation, the calling span becomes the parent and the called span becomes the child.
- Context propagation --> how information about a trace is passed between different services and systems.
	- ensures that all parts of a distributed system can contribute to a single trace
- Instrumentation --> add code to applications or services in order to generate traces and spans.
	- can be manual or automatic, depending on whether it requires developers to add code explicitly, or relies on libraries or frameworks to do so automatically.
#### <span style="color:#689d6a">Observability</span>
---
Observability is a term used in engineering and computer science to describe the ability to understand the internal state of a system using its external output

It refers to the extent to which we can infer what's happening within a system by examining its external behavior

An observable system is one that provides sufficient information about its internal workings to allow operators and developers to diagnose issues and understand how it behaves under different circumstances.

The goal of observability is to enable faster identification and resolution of issues, ultimately leading to more reliable and efficient systems.

It involves not just collecting data but also analyzing in real time and using it to gain deeper insights into how a system is functioning.

It allows teams to quickly identify and resolve issues in complex systems by providing context rich information that helps them understand how the different parts of the system are interacting

is a proactive approach --> checking real-time system behavior, with minimal pre-definition of what to look for.

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

Logs --> record of events
- contain details of the application's request processing stages
- capture information about individual events or transactions
- exceptions provide indicators of problems
- monitoring errors and exceptions are a part of the solution
- parsing logs provide application performance insights
- Advantages:
	- easy generate format: timestamp + payload
	- no explicit integration is required
	- often plain text and human-readable
	- allows retrospective replaying of support incidents

Metrics --> real-time operating data
- numerical measurement showing component health
- provide aggregated system performance data
- collection is intuitive
- collection and analysis requires great care
- Advantages:
	- quantitative and intuitive
	- lightweight and cheap to store and retrieve
	- great at tracking and understanding
	- good at understanding changing systems or services

Traces --> information pathways or workflows records
- data from multiple components stitched together
- shows end-to-end workflow of a request
- breaks down end-to-end latency
- identifies bottlenecks
- Advantages:
	- perfectly identifies the problematic component or step
	- debug issues in a distributed system
	- context-specific details about the system's behavior
	- provides context-specific details about system behavior
##### <span style="color: #d79921">Cloud native observability</span>

Is the practice of monitoring and understanding the behavior of cloud-native applications running in dynamic and distributed environments. It involves collecting, processing, analyzing and visualizing large amounts of data.

Cloud native observability utilizes techniques like metrics logs, traces, events, and alerts to provide a holistic view of the system.

The goal is to enable DevOps teams to swiftly detect and effectively troubleshoot issues and continuously enhance the application delivery process.

Pillars of cloud observability
- Automation --> Automatic and continuous detection of changes
- Context --> Interconnections between applications components and services
- Intelligent action --> provides deep analysis and suggestions for system optimization

Cloud observability tools
- An effective cloud native observability tool --> correlates data across cloud environments
	- provides a single, intuitive interface
	- readdresses application performance issues
	- focuses on comprehensive visibility
	- ensures seamless user experience
- --> Traditional monitoring tools and solutions may lack the necessary instrumentation, connectivity, and observability features required for modern Cloud ecosystems.
- Obs: organizations having cloud-based technologies require a cloud native observability tool.
- The best-suited observability tool must enable organizations to maximize the benefits of modern applications, enhance customer experiences, and improve business outcomes.
- The ideal tool or solution must strengthen organization's infrastructure security, afeguard sensitive customer data, optimize performance, and achieve business success.
- Popular tools:
	- Jaeger
		- project under CNCF
		- aims to address the challenges of developing distributed systems
		- challenging to monitor and debug transactions for more distributed networks
	- Fluentd
		- A logging system designed to be decoupled from the backend system
		- solves the incompatibility problem by unifying logging formats
		- solves routines through its unified logging layer
	- Thanos
		- provides extended capabilities for organizations seeking more from Prometheus
		- enables unlimited storage capacity for Prometheus deployments
		- Allows organizations utilizing multiple Prometheus servers and clusters access to global metrics views.
	- New Relic
		- a full stack, all-in-one cloud-based observability platform
		- provides insights into: application performance, infrastructure health, user experience.
	- AWS CloudWatch
		- a monitoring service provided by Amazon Web Services (AWS)
		- provides metrics on resources and applications running on AWS
	- Google Cloud Monitoring
		- a monitoring service provided by Google Cloud Platform (GCP)
		- provides visibility into infrastructure and applications performance across GCP services

Benefits:
- Detect and fix issues efficiently
- Reduced MTTR (mean time to repair) by identifying correlations between events
- Shift left to diagnose issues earlier in the development cycle
- Healthier system with fewer errors and more efficient processes
##### <span style="color: #d79921">Sampling</span>

Sampling and logging is a practice of collecting only a subset of log events/records for analysis or storage. Instead of logging every single event or piece of data, a subset is selected at random or by some other criteria for recording.

Sampling in logging infrastructure --> optimize log processing and reduce cost

Strategies
- --> Refer to the techniques used to select a subset of log records for analysis and storage.
- Time-based sampling --> log records at fixed time intervals
- Size-based sampling --> Log records based on size
- Random sampling --> Log records from a larger set
- Event-based sampling --> Log records based on specific events
- Weighted sampling --> Log records based on their relevance

Examples:
- CPU sampling --> to determine its performance characteristics
- Network packet sampling --> collecting a sample of network packets flowing through the network to identify issues with the network traffic
- Sampling tracing data --> helps in identifying bottlenecks and other issues from distributes systems
- Log sampling --> collecting logs from various sources across the system, sampling them for analysis and identifying unusual trends or patterns.
- Error rates sampling --> identifying and sampling errors generated by an application to trace down critical issues that need immediate attention.
- User behavior sampling --> analyzing user behavior through sampling data such as click streams, mouse movements, and other user interactions to improve the user experience.

Benefits: reduced overhead, enhanced performance, cost-effective, improved accurary, better scalability.
##### <span style="color: #d79921">IBM Instana Obervability</span>

Instana, is a fully automated application performance management, or APM solution. Designed to overcome the challenges of managing microservices and cloud-native applications.

Makes the applications and services visible

Provides context to the observed information

Enables taking intelligent actions

Use cases:
- Monitor and analyses: applications, services, infrastructure, web browsers, mobile applications.
- Automates dependency mapping across the full stack
- Provides powerful and easy-to-use data analytics
- Highlights when customers are impacted by performance or stability issues
- Automates root-causes analysis
- Uses event correlation, performance thresholds, errors, changes, SLA violations
- Provides real-time observability metrics with data at a granularity of 1 second
- Traces every second end-to-end mobile, web, and, application transaction

Features:
- --> Instana monitors over 200 technologies, such as technologies related to cloud and infrastructure, tracing, alerting, notifications, CI/CD logging and metrics.
- infrastructure map --> provides an overview of all monitored systems grouped by named zones.
- each pillar --> represents one agent running on the respective system
	- each block within the pillars represents the software components running on that system
	- change color to reflect the component's health
- dashboard --> show physical components, such as a data center or availability zones
- Instana agents --> monitor the technology stacks
- Instana sensors --> designed to monitor specific technologies
	- automatically installed
- Website monitoring --> tool for understanding digital user experience
	- Instana supports website monitoring by analyzing actual browser request times and route load times
- Instana's unbounded analytics provides infinite flexibility to generate new insights from all unsampled high cardinality data.
- Custom events can be configured, which trigger custom issues
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

Choose a tracing tool - instrument the code - configure the tracing agent - deploy the tracer - verify functionality

Distributed tracing tracks the flow of application requests from front-end component or devices to back-end services, databases, and other third-party services.

Best practices: instrument services with code, implement end-to-end instrumentation and record traces, pay attention to duration metrics, follow OpenTelemetry, OpenTracing and OpenCensus standardization. 