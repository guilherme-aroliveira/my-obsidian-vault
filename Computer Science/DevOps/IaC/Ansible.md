Created by Michel DeHann the create of Cobbler, and purchased by Red Hat in 2015.
Integrated into Fedora and Red Hat Enterprise Linux 8. Ansible is writren in Python

Ansible maintains ainventory of host to work agaisnt. It then selects protions of the onventory wich sre sotee ins ASCII text files. 

Any machine with Ansible installed can leveage a set of files and direcotires to orchestrate other nodes.

with ansible we can manage a node's opertatign sysem configuration including intalled pakacges, device configurations, user, groups, ect..

ansible configurations are simple data descriptions of a infrastructure in a huam readable format. It only requres a password or SSH key to manage a system.

ansible follows a state-driven resource model taht describes teh desired state of the computer or service, not the path to get to the state. It can do a "dry run" test , which allow it to run through the process withotu actually changing the state of the node or nodes.

It relies on OpenSSH and does not use remote agents.

All ansible modules run with user-supplied creadentials, includign support for sudo, or even kerberos and then clena themselves up when complete. It does not requie root login privileges. 

Control hosts can use multiple inventory files at the same time

Nodes are managed by the controlling machine over SSH

ansible can work with multiple systems at the same time, it uses ssh and powershell. 
no addition software needs to be installed on the target machine.
ansible requires python

Ansible works agains multiple nodes or hosts at the same time. The list of nodes is called an inventory, and can be static or dynamic. the default inventory file locarion is `/etc/ansible/hosts`
the inventory describes the location of nodes. Sensite data can be stored in encrypted files by using ansible vault
to specify a different static inventory file:
`ansible-plabook -i hosts.txt`
more than one static file can be used at the same time
`ansible-plabook -i hosts.txt -i groups.txt`
--> if there's a conflict in the two files the variables in the latter file will be used. Example variables in production will override thowse in staging because it's processed last.
`ansible-plabook deploy_web.yaml -i satging -i productuin`

inventory is a description of the nodes that can be accessed by Ansible. Ny default the inventory is described in INI or Yaml formart. It conaints IP address or hostname of each node.
nodes caneb assigned to groups
INI --> simples file

ansible is agentless --> no sfteare agent running on the nodes consuming resources.
ansible orchestratea node by installig and runnimg modules on the nide temproraily via SSH.

For the duration of the orchestration task, the running modules task communicates, with a JSON based protocol via standard input and ouptut --> stand alone mofules th cna be written in standard scripnt ing laguages like Python, Ruby, Perl or bash,

Ansible module sare support to presibre to idempotency

idempotency --> an operation cane be run multiple times an the resulting state is always the same.

ansible work gaist multiple node or hosts at the same time. This list if de is called inventory and can be static or dynamic.

For windows nodes native powerhsel remoting supported by the WS-management protocol is used instead of SSH

the options in the `.asible.cfg` file in the user's home directory, will override the global one listed in the `/etc/ansible/.asible.cfg`

`ssh-copy-id IP_address` --> to copy the public to the host2
`ansible -m ping all` --> to test the communication with the node

ANsible has a large selection of modues specifically aimed ar provisioning virtual environments
ansible network automation allows us to configure, validate,  and ensure continuous compliance for physical network devices --> it can replace manual processes for provisioning networks.
ansible can provision and manage infrastrcuture storage systems including software software-defned storeage, cloud-based storeage, and even hardware storage appliances. 

information about the target systems is store in an inventory file
the default inventory file is at `/etc/ansible/hosts`
`ansible-playbook -i` --> provide a different static inventory file
- Example: `ansible-playbook -i /home/user1/hosts`
- more that one static inventor file can be used at the same time

static inventory:
to test add to `/etc/ansible/hosts`:
add to host1 the host2 IP address. 
Ex: `192.168.3.110 rhost2 rhost2.localnet.com` 
`ping -c1 rhost2`
`ping -c1 rhost2.localnet.com`

The inventory file can be in one of many different formats depending of the inventory plug-ins that are installed. the cost common formats are INI and YAML
INI --> simplet format
```ini
192.168.6.1

[webservers] # node group
web1.localnet.com
web2.localnet.com

[dbservers]
db1.localnet.com
db2.localnet.com
db3.localnet.com
```

```ini
192.168.6.1

[mail]
server2.company.com
server3.company.com

[web] # node group
server4.company.com
server5.company.com

[db]
server6.company.com
server7.company.com
```

ANaible can also use a custom dynamic inventory script wth pulls data from a different system and supportds froups of groups

It uses plabooks to manage configurarion ot task on nodes, A playbook is a yaml file that expresses the configurations, deplpyment, and orchestration and they allow Ansible to performam operations on nodes.

Each playbooks maps a group of host to set of roles. Each role is represented to call by Ansible tasks.

>[!example] Example - Playbook
>```yaml
>- hosts: webservers
>  vars:
>    http_port: 80
>    max_clients: 200
>  remote_use: not
>  tasks:
>  - name: ensure apache is at the latest version
>    yum: 
>     name: httpd
>     state: latest
>```

group names --> used in classifying hosts and deciding which host to control at one time.
inventory file in yaml format
```yaml
all:
  hosts:
    mail.localnet.com
  children:
    webservers:
      hosts:
        web1.localnet.com
        web2.localnet.com
    dbservers:
      hosts:
        db1.localnet.com
        db2.localnet.com
        db3.localnet.com
```

default groups
- all group  --> contains every host
- ungrouped group --> contains all hosts that don't belong to another group

every host will always belong to at least two groups, or all and ungrouped, or all and a specific group.

Often groups are categorized in 
what - the service a host provides, such as WEB or DNS
where - a host's location 
when - development stage, test stage or prod stage.

```yaml
seattle: # where
	web1.localnet.com
	db1.localnet.com
sanfranciso:
	web2.localnet.com
	db2.localnet.com
prod: # when
	web1.localnet.com
	web2.localnet.com
	db1.localnet.com
	db2.localnet.com
test:
	web3.localnet.com
	db3.localnet.com
```

nested inventory

```yaml
seattle: # where
	web1.localnet.com
	db1.localnet.com
sanfrancisco:
	web2.localnet.com
	db2.localnet.com
prod: # when
	children:
		sanfrancisco
test:
	children:
		seattle:
```

using numeric ranges

```yaml
all:
  hosts:
    mail.localnet.com
  children:
    hosts:
      webservers:
        hosts:
          web[1:3].localnet.com:
      dbservers:
        hosts:
          db[1:3].localnet.com:
```


To access a host on a non-standard ssh port:
```ini
[webserver]
web1.localnet.com:1022
web2.localnet.com:1022
```


To access the manual pages within the terminal 'ansible-doc' is a good for pulling documentation on Ansible plugins and modules. 

configuration file order:
location in $ANSIBLE_CONFIG
`./ansible.cfg`
`ansible.cfg` in the user directory
`/etc/ansible/ansible.cfg`
ansible variable set in playbooks override all other methods. Variable are set in playboks using the `vars` keyword:
```yaml

```

ansible variables can also be assigned on the command line:

```shell
ansible -e ansible_user=user2
```

OS environment variables have a higher precedence that entries in any of the `ansible.cfg` files.
command line options like environment variables will also override any settings in the `Ansible.cfg`. Configuration data can also be included in Ansible keywords. 

configure the host server
`ansible all --list-hosts` --> the inventory
copy the pub key to another server: `ssh-copy-id <IP_address>`
ansible -m ping all --> communicate with the server
ansible -a --> to send regular linux command
- `ansible -a "uptime" all`
`ansible-doc -l` --> list of all available modules
- `ansible-doc -t cache -l` --> narrow the list
`ansible-doc -s file` --> get a snippet of the doc page, list the option dor the module with description

plugin types
become --> for privelege escalation
cache --> for backing cacnhing
callback --> enables adding new behaviors and reponding to events
clinconf --> provides an interface for executing tasks on network devices
connection --> used to connect to targets
httpapi --> interacts with a remote device's HTTP based API
inventory --> points at data source for inventory
lookup --> allows Ansible to access data from outside sources
netconf --> provides an interface to execute tasks on netconf devies
shell --> ensure that the commands are properly formatted modules
strategy --> controls the flow of play execution
vars --> inject additional variable data into Ansible runs that did not come from inventory source, playbook or command line. 

using alias
`web    ansible_host=server1.company.com`
`ansible_host` --> inventory parameter used to specify the FQDN or IP address of a server
ansible_connection --> defines how ansible connects to the target server. example: `ansible_connection=ssh`, `ansible_connection=ssh/winrm/localhost
ansible_port - 22/5986 --> defines witch port to connect to, By default. It is set to port 22 for SSH
ansible_user - root/administrator, defines the user used to make remote connections by default. This is set to root for Linux machines.
ansible_ssh_pass - password, defines the ssh password for Linux.

localhost ansible_connection=localhost --> indicate that we would like to work with the local host and not connect to any remote host

The best practice is to set up SSH key based passwordless authentication between the servers.

Is an open-source tools that automates IT tools such as infra-service orchestration, application deploy, cloud provisioning, etc. It uses familiar yaml files to describe the state to be achieved. It doesn't require any client-side agents.

Ansible use ssh to establish connection with multiple servers --> it's agentless, there's no need to install any software on the target machine to be able to work with ansible

An Ansible playbook or a rule can be checked into a version control repository

Ansible playbooks are Ansible, orchestration, language. It is in playbooks where we define what we want Ansible to do. It is a set of instructions.
For example, it can be as simple as running a series of commands on different servers in a sequence and restarting those servers in a particular order.

all playbooks are written in YAML format. A playbook is a single YAML file containing a set of plays. A play defines a set of activities to be run on a single or a group of hosts. A task is a single action to be performed on a host.
Some examples of a task are executing a command or a script on the host.

>[!example] Example - playbook.yaml
>```yaml
>name: Play1
>hosts: localhost
>tasks:
>  - name: Execute command 'date'
>     command: date
>     
>  - name: Execute script on server
>  - command: test_script.sh
>
>  - name: Install httpd service
>    yum: # module
>      name: httpd
>      state: present
>  
>  - name: start web server
>    service: # module
>      name: httpd
>      state: started
>```

So the playbook is a list of dictionaries in YAML terms.
The tasks, as you can see, is a list or an array as denoted by the dashes.
Lists are ordered collection, so the position of entries matter.

the host parameter indicates which host you want these operations to run on

The host defined in the inventory file must match the host used in the playbooks and all connection information for the host is retrieved from the inventory file.

The different actions run by tasks are called modules

`ansible playbook playbook.yaml`

`ansible-playbook -i inventory playbook.yaml`

The goal of this play is to run a set of activities one after the other on the local host. The host you want to run these actions is defined at the play level.

Inventory file --> stores information about the target system, the default inventory is located at /etc/ansible/hots. It can group multiple servers by type.

ansible tower -- a REST API, web service, and wbe based console desiged to make Ansible more usable for IT teams. It's a hub for automation tasks and it helps to manage inventory.

`ansible-inventory --list -i aws_inventory.py`  --> list all hosts

##### ansible modules

Ansible modules are categorized into various groups based on their functionality.
Example: System, Commands, Files, Database, Cloud, Windows, ...


System modules are actions to be performed at a system level, such as modifying the users and groups
on the system, modifying IP tables, firewall configurations on the system, working with logical volume
groups, mounting operations or working with services, for example, starting stopping or restarting
services in a system, command modules are used to execute commands or scripts on a host.

command modules are used to execute commands or scripts on a host.
This could be simple commands using the command module or an interactive execution using the ECS module.

File modules help work with files.
For example, use the ACL module to set and retrieve ACL information on files.
Use the archive and archive modules to compress and unpack files, use find lining file and replace modules to modify the contents of an existing file.

Database modules help in working with databases such as MongoDB, MySQL, MySQL or PostgreSQL to add or remove databases or modify database configurations.
  
The cloud section has a vast collection of modules for various different cloud providers like Amazon, Azure, Docker, Google, OpenStack and VMware being just a few of them.

And then there are Windows modules that help you use Ansible in a Windows environment. Some of these are `Win_copy` to copy files, `Win_command` to execute a command on a Windows machine.

command module

```yaml
tasks:
  - name: Execute command 'date'
    command: date
     
  - name: Execute script on server
    command: test_script.sh
```

the copy module which is used to copy files from a source to a destination, only takes parameterized input.

```yaml
tasks
  - name:
    copy: 
```

script module
executes a script which is located locally on the Ansible controller machine on one
or more remote nodes after transferring it over 

```yaml
name: Play1
hosts: localhost
tasks:
  - name: 
    script: /some/local/script.sh -arg1 -arg2

```

Ansible takes care of automatically copying the script to the remote node and then executing it on the remote systems.

service module
The service module is used to maintain services on a system such as starting stopping or restarting a service.
Then the service module, unlike the previous modules, do not have a free form input, which means you have to pass input in a key value pair format.
We use the name parameter to specify the name of the service we wish to start.
Now, there are two ways of writing this statement.
You can either write it like this or write it in a dictionary or a map format like this.
They're one and the same.

Remember in YAML terms, name and state are properties of service.

```yaml
name: Start Services in order
hosts: localhost
tasks:
  - name: Start the database service
    service: name=postgresql state=stated
```

```yaml
name: Start Services in order
hosts: localhost
tasks:
  - name: Start the database service
    service: 
      name=postgresql 
      state=stated
```

Instead, we are instructing Ansible to ensure that the service httpd is started.

lineinfile
is used to find a line in a file and replace it or add it if it doesn't already exist

For example, we are given a task to add a new DNS server into the `/etc/resolv.conf` file.

```yaml
name: Add DNS server to resolv.conf
hosts: localhost
tasks:
  - lineinfile:
      path: /etc/resolv.conf
      line: 'nameserver 10.1.250.10'
```
If you run the Ansible playbook multiple times, it will ensure there is only a single entry in the file.
##### ansible variables

It's the variables that store information about the different host names, usernames or passwords that are different for each server.

To add a variable, we could simply add a var directive followed by variables in a key value pair format.
We can also have variables defined in a separate file dedicated for variables.

```yaml
name: Add DNS server to resolv.conf
hosts: localhost
vars:
  dns_server: 10.1.250.10
tasks:
  - lineinfile:
      path: /etc/resolv.conf
      line: 'nameserver {{ dns_server }}'
```

And even better way to do this would be to move the variables into a file in the name of the host

>[!example] Example - variables with external file
>```yaml
># Sample variable File - web.yaml
>http_port: 8081
>snmp_port: 161-162
>inter_ip_range: 192.0.2.0
>```
>---
>```yaml
>name: Set Firewall Configurations
>hosts: web
>tasks:
>- firewalld:
>    service: '{{ http_port}}'/tcp
>    permanent: true
>    state: disabled
>    
>- firewalld:
>    service: '{{ snmp_port}}'/udp
>    permanent: true
>    state: disabled
>```

Remember this format we are using to use variables in playbooks is called Jinja2 Templating.
##### ansible conditions

I could use the when conditional statement to specify a condition for each task.
Only if the condition is true, that task is run.

```yaml
- name: Install NGINX
  hosts: all 
  tasks:
  - name: Install NGINX on Debian
    apt:
      name: nginx
      state: present
    when: ansible_os_family == "Debian" and
          ansible_distribution_version == "16.04"

  - name: Install NGINX on Redhat
    yum:
      name: nginx
	  state: present
	when: ansible_os_family == "Redhat" or 
	      ansible_os_family == "SUSE"  
```

You may use conditionals in a loop as well.

```yaml
- name: Install Softwares
  hosts: all 
  vars:
    packages: 
      - name: nginx
        required: True
      - name: mysql
        required: True
      - name: apache
        required: True
  tasks:
    - name: Install "{{ item.name }}" on Debian
      apt:
        name: "{{ item.name }}"
        state: present
      when: item.required == True
      loop: "{{ packages }}"
```

To use conditionals with the output of a previous task, we have a requirement to develop a playbook to check the status of a service and email if it's done.

```yaml
- name: Check status of a service and email if its down
  hosts: localhost
  tasks:
   - command: service httpd status
     register: result

   - mail: 
      to: admin@company.com
      subject: Service Alert
      body: Httpd Service is down
      when: result.stdout.find('down') != -1
```

##### ansible loops

Loop is a looping directive that executes the same task multiple number of times each time it runs.

```yaml
name: Create users
hosts: localhost
tasks:
  - user: 
      name='{{ item }}' 
      state=present
    loop:
      - joe
      - george
      - ravi
      - mani
```

 with directives
with items. Just iterates over a list of items.

```yaml
name: View config file
hosts: localhost
tasks:
  - debug: var=item
    with_file:
      - "/etc/hosts"
      - "/etc/resolv.conf"
      - "/etc/ntp.conf"
```

```yaml
name: Check multipl mongodbs
hosts: localhost
tasks:
  - debug: msg="DB={{ item.database}} PID={{ item.pid }}"
    with_mongodb:
      - database: dev
        connection_string: "mongodb://dev.mongo/"
      - database: prod
        connection_string: "mongodb://prod.mongo/"
```

In fact, everything you see after the with underscore string is a lookup plugin --> ustom scripts that can do specific tasks like read files, connect to a URL or connect to a database or connect to other systems like Kubernetes or OpenShift.

##### ansible roles

the primary purpose of roles to make your work reusable, be it for other tasks or projects within your organization or outside for others globally.

Roles also help in organising your code within Ansible.

Roles introduce a set of best practices that must be followed to organize all tasks into a task directory.

