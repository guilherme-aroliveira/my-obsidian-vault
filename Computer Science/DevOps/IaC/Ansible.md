Is an open-source tools that automates IT tools such as infra-service orchestration, application deploy, cloud provisioning, etc. It uses familiar yaml files to describe the state to be achieved. It doesn't require any client-side agents.

Ansible use ssh to establish connection with multiple servers --> it's agentless, there's no need to install any software on the target machine to be able to work with ansible

An Ansible playbook or a rule can be checked into a version control repository

Inventory file --> stores information about the target system, the default inventory is located at /etc/ansible/hots. It can group multiple servers by type.