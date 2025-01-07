
ansible can work with multiple systems at the same time, it uses ssh and powershell. 
no addition software needs to be installed on the target machine.
ansible requires python

ansible work gaist multiple node or hosts at the same time. This list if de is called inventory and can be static or dynamic.

information about the target systems is store in an inventory file
the default inventory file is at `/etc/ansible/hosts`
`ansible-playbook -i` --> provide a different static inventory file
- Example: `ansible-playbook -i /home/user1/hosts`
- more that one static inventor file can be used at the same time

The inventory file can be in one of many different formats depending of the inventory plug-ins that are installed. the cost common formats are INI and YAML
INI --> simplet format
```ini
mail.localnet.com

[webservers] # group names
web1.localnet.com
web2.localnet.com

[dbservers]
db1.localnet.com
db2.localnet.com
db3.localnet.com
```
group names --> used in classifying hosts and deciding which host to control at one time.

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
`ansible_host` --> inventory parameter used to specify the IP address of a server
ansible_connection --> defines how ansible connects to the target server. example: `ansible_connection=ssh`, `ansible_connection=winrm`
ansible_port
ansible_user
ansible_ssh_pass

Is an open-source tools that automates IT tools such as infra-service orchestration, application deploy, cloud provisioning, etc. It uses familiar yaml files to describe the state to be achieved. It doesn't require any client-side agents.

Ansible use ssh to establish connection with multiple servers --> it's agentless, there's no need to install any software on the target machine to be able to work with ansible

An Ansible playbook or a rule can be checked into a version control repository

Inventory file --> stores information about the target system, the default inventory is located at /etc/ansible/hots. It can group multiple servers by type.

